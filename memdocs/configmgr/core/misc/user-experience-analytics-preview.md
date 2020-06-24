---
title: Preview van endpoint Analytics
titleSuffix: Configuration Manager
description: Instructies voor de preview-versie van endpoint Analytics.
ms.date: 06/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 00537b90-f6d2-45e9-a9a1-6b3ada466a16
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: f33f79d1a2fb6144e25d6153c48caa90d86006e6
ms.sourcegitcommit: 97f150f8ba8be8746aa32ebc9b909bb47e22121c
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/17/2020
ms.locfileid: "84879765"
---
# <a name="endpoint-analytics-preview"></a><a name="bkmk_uea"></a>Preview van endpoint Analytics

> [!Note]  
> Deze informatie is gekoppeld aan een preview-functie die aanzienlijk kan worden gewijzigd voordat deze commercieel wordt uitgebracht. Microsoft biedt geen enkele expliciete of impliciete garanties met betrekking tot de informatie die hier wordt verstrekt. 
>
> Zie [what's New in endpoint Analytics](whats-new-endpoint-analytics.md)(Engelstalig) voor meer informatie over wijzigingen in endpoint Analytics. 
>
>Als u wilt deel nemen aan de persoonlijke Preview voor endpoint Analytics, voert u de gegevens [in dit formulier in](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9-ZzmlTlbJMh03eDDHtO81UOERLUkMzNFZKSlBaNFNFUVhFSlE0MzNYMS4u). Tenants worden in vlucht gegeven als openingen voor de preview-versie.


## <a name="endpoint-analytics-overview"></a>Overzicht van eindpunt analyse

Het is niet ongebruikelijk dat eind gebruikers langdurige opstart tijden of andere onderbrekingen kunnen ervaren. Deze onderbrekingen kunnen worden veroorzaakt door een combi natie van:

- Oudere hardware
- Software configuraties die niet zijn geoptimaliseerd voor de ervaring van de eind gebruiker
- Problemen die worden veroorzaakt door configuratie wijzigingen en updates

Deze problemen en andere problemen met de eind gebruikers ervaring blijven bestaan omdat deze niet veel inzicht in de ervaring van de eind gebruiker heeft. Over het algemeen is de enige zicht baarheid van deze problemen afkomstig van een langzaam ondersteunings kanaal dat doorgaans geen duidelijke informatie biedt over wat er moet worden geoptimaliseerd. Het is niet alleen IT-ondersteuning die de kosten van deze problemen ondervindt. De tijd die IT-mede werkers best Eden aan problemen, is ook kostbaar. Problemen met prestaties, betrouw baarheid en ondersteuning die de productiviteit van de gebruiker verminderen, kunnen ook grote gevolgen hebben voor de onderste lijn van een organisatie.

**Endpoint Analytics** is erop gericht om de productiviteit van gebruikers te verbeteren en de IT-ondersteunings kosten te verlagen door inzicht te bieden in de gebruikers ervaring. Met de inzichten kunnen IT de eindgebruikers ervaring optimaliseren met proactieve ondersteuning en kunnen er regressies worden gedetecteerd voor de gebruikers ervaring door de invloed van de configuratie wijzigingen te beoordelen.

Deze eerste release is gericht op drie dingen:

- [**Aanbevolen software**](#bkmk_uea_rs): aanbevelingen voor het bieden van de beste gebruikers ervaring
- [**Proactief herstel scripting**](#bkmk_uea_prs): veelvoorkomende ondersteunings problemen oplossen voordat eind gebruikers problemen ondervinden
- [**Prestaties opstarten**](#bkmk_uea_bp): Hiermee kunnen gebruikers snel aan de slag met productiviteit zonder langdurige opstart-en aanmeldings vertragingen

Deze versie is slechts het begin. Binnenkort gaan we nieuwe inzichten in op andere belang rijke gebruikers ervaringen, kort na de eerste release. Zie [what's New in endpoint Analytics](whats-new-endpoint-analytics.md)(Engelstalig) voor meer informatie over wijzigingen in endpoint Analytics.

## <a name="getting-started"></a><a name="bkmk_uea_prereq"></a>Aan de slag

Als u endpoint Analytics wilt gaan gebruiken, controleert u de vereisten en gaat u vervolgens gegevens verzamelen. 

### <a name="technical-prerequisites"></a>Technische vereisten

Voor deze preview kunt u apparaten inschrijven via Configuration Manager of Microsoft Intune. 

#### <a name="to-enroll-devices-via-intune-this-preview-requires"></a><a name="bkmk_uea__intune_prereq"></a>Als u apparaten wilt registreren via intune, moet u voor deze preview-versie het volgende doen:
- InTune Inge schreven apparaten met Windows 10
- Prestatie inzichten voor opstarten zijn alleen beschikbaar voor apparaten met versie 1903 of hoger van Windows 10 Enter prise (Home-en Pro-edities worden momenteel niet ondersteund) en de apparaten moeten worden toegevoegd aan Azure AD of hybride Azure AD. Machines die aan de werk plek zijn gekoppeld, worden momenteel niet ondersteund.
- Netwerk verbinding van apparaten met de open bare cloud van micro soft. Zie [eind punten](#bkmk_uea_endpoints)voor meer informatie.
- De [intune-service beheerdersrol](https://docs.microsoft.com/intune/fundamentals/role-based-access-control) is vereist om te beginnen met het [verzamelen van gegevens](#bkmk_uea_start).
   - Door te klikken op **Start**, gaat u akkoord met en erkent u dat uw klant gegevens kunnen worden opgeslagen buiten de locatie die u hebt geselecteerd tijdens het inrichten van uw Microsoft intune-Tenant.
   - Nadat u op **starten** voor het verzamelen van gegevens hebt geklikt, kunnen andere alleen-lezen rollen de gegevens weer geven.

#### <a name="to-enroll-devices-via-configuration-manager-this-preview-requires"></a><a name="bkmk_uea__cm_prereq"></a>Als u apparaten wilt registreren via Configuration Manager, is voor deze preview het volgende vereist:
- Configuration Manager versie 2002 of hoger
- Clients bijgewerkt naar versie 2002 of hoger
- [Micro soft Endpoint Manager-Tenant koppelen](https://docs.microsoft.com/mem/configmgr/tenant-attach/device-sync-actions) is ingeschakeld.

#### <a name="proactive-remediation-scripting-requires"></a><a name="bkmk_uea__prs_prereq"></a>Voor proactieve herstel scripting is het volgende vereist:
Bij het inschrijven van apparaten via intune of Configuration Manager, hebben [**proactieve herstel scripts**](#bkmk_uea_prs) de volgende vereisten:
- Apparaten moeten lid zijn van Azure AD of hybride Azure AD zijn toegevoegd en voldoen aan een van de volgende voor waarden:
- Een Windows 10 Enter prise-, Professional-of Education-apparaat dat wordt beheerd door intune
- Een [gezamenlijk beheerd](../../comanage/overview.md) apparaat met Windows 10 Enter prise, versie 1607 of hoger met de [werk belasting](../../comanage/workloads.md#client-apps) van de client-apps naar intune.
- Een [gezamenlijk beheerd](../../comanage/overview.md) apparaat met Windows 10 Enter prise, versie 1903 of hoger met de [werk belasting](../../comanage/workloads.md#client-apps) van de Client-apps naar Configuration Manager.

### <a name="licensing-prerequisites"></a>Licentie vereisten

Endpoint Analytics is opgenomen in de volgende abonnementen: 

- [Enterprise Mobility + Security E3](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) of hoger
- [Microsoft 365 Enterprise E3](https://www.microsoft.com/en-us/microsoft-365/enterprise?rtc=1) of hoger.

Voor proactieve herstel bewerkingen is ook een van de volgende licenties vereist voor de beheerde apparaten:
- Windows 10 Enter prise E3 of E5 (opgenomen in Microsoft 365 F3, E3 of E5)
- Windows 10-onderwijs a3 of A5 (opgenomen in Microsoft 365 a3 of A5)
- Windows Virtual Desktop Access E3 of E5

### <a name="permissions"></a>Machtigingen

#### <a name="endpoint-analytics-permissions"></a>Eindpunt Analytics-machtigingen

De volgende machtigingen worden gebruikt voor endpoint Analytics:
- **Lees** de categorie **device configurations** .
- **Lees** de categorie **organisatie** . <!--temporary for pp-->
- Machtigingen die van toepassing zijn op de rol van de gebruiker onder de categorie **endpoint Analytics** .

Een alleen-lezen gebruiker heeft alleen de machtiging **lezen** nodig onder de klassen **configuraties** en **endpoint Analytics** . Een intune-beheerder heeft normaal gesp roken alle machtigingen nodig.

#### <a name="proactive-remediations-permissions"></a>Machtigingen voor proactieve herstel bewerkingen

Voor proactieve herstel bewerkingen heeft de gebruiker machtigingen nodig voor hun rol in de categorie **apparaat-configuraties** .  Machtigingen in de categorie voor het **endpoint Analytics** zijn niet nodig als de gebruiker alleen proactieve herstel bewerkingen gebruikt.

De [intune-service beheerder](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#intune-service-administrator-permissions) moet de licentie vereisten bevestigen voordat proactieve herstel bewerkingen voor de eerste keer worden gebruikt.

## <a name="start-gathering-data"></a><a name="bkmk_uea_start"></a>Gegevens verzameling starten
- Als u alleen door intune beheerde apparaten wilt registreren, gaat u naar de [onboarding in het gedeelte endpoint Analytics-Portal](#bkmk_uea_onboard) .

- Als u apparaten registreert die worden beheerd door Configuration Manager, moet u de volgende stappen uitvoeren:
   - [Gegevens verzameling voor endpoint Analytics inschakelen in Configuration Manager](#bkmk_uea_cm_enroll)
   - [Het uploaden van gegevens in Configuration Manager inschakelen](#bkmk_uea_cm_upload)
   - [Onboarding in de Endpoint Analytics-Portal](#bkmk_uea_onboard)  

### <a name="enroll-devices-managed-by-configuration-manager"></a><a name="bkmk_uea_cm_enroll"></a>Apparaten registreren die worden beheerd door Configuration Manager
<!--6051638, 5924760-->
Voordat u Configuration Manager-apparaten inschrijft, controleert u de [vereisten](#bkmk_uea_prereq) , waaronder het inschakelen van [micro soft Endpoint Manager-Tenant bijvoegen](https://docs.microsoft.com/mem/configmgr/tenant-attach/device-sync-actions). 

#### <a name="enable-endpoint-analytics-data-collection-in-configuration-manager"></a><a name="bkmk_uea_cm_enable"></a>Gegevens verzameling voor endpoint Analytics inschakelen in Configuration Manager

1. Ga in de Configuration Manager-console naar de client instellingen voor de **beheerders**  >  **Client Settings**  >  **instelling**.
1. Klik met de rechter muisknop en selecteer **Eigenschappen** en selecteer vervolgens de instellingen van de **computer agent** .
1. Stel **endpoint Analytics-gegevens verzameling inschakelen** in op **Ja**.
   > [!Important] 
   > Als u een bestaande aangepaste client agent hebt ingesteld die op uw apparaten is geïmplementeerd, moet u de optie voor het **verzamelen van endpoint Analytics-gegevens** in deze aangepaste instelling bijwerken en vervolgens opnieuw implementeren op uw computers om deze van kracht te laten worden.

#### <a name="enable-data-upload-in-configuration-manager"></a><a name="bkmk_uea_cm_upload"></a>Het uploaden van gegevens in Configuration Manager inschakelen

1. Ga in de Configuration Manager-console naar **beheer**  >  **Cloud Services**  >  **co-beheer**.
1. Selecteer **CoMgmtSettingsProd** en klik vervolgens op **Eigenschappen**.
1. Schakel op het tabblad **Upload configureren** de optie in om **endpoint Analytics in te scha kelen voor apparaten die zijn geüpload naar micro soft Endpoint Manager**

   :::image type="content" source="media/6051638-configure-upload-configmgr.png" alt-text="Endpoint Analytics inschakelen voor apparaten die zijn geüpload naar micro soft Endpoint Manager" lightbox="media/6051638-configure-upload-configmgr.png":::

### <a name="onboard-in-the-endpoint-analytics-portal"></a><a name="bkmk_uea_onboard"></a>Onboarding in de Endpoint Analytics-Portal
Het voorbereiden van de portal voor het endpoint Analytics is vereist voor zowel Configuration Manager als door intune beheerde apparaten.

1. Ga naar `https://aka.ms/endpointanalytics`
1. Klik op **Start**. Hiermee wordt automatisch een configuratie profiel toegewezen voor het verzamelen van opstart prestatie gegevens van alle apparaten die in aanmerking komen. U kunt later [toegewezen apparaten wijzigen](#bkmk_uea_profile) . Het kan tot 24 uur duren voordat de prestatie gegevens van uw intune-apparaten zijn Inge schreven nadat de computer opnieuw is opgestart.

> [!Important]  
> We anoniem makenen de scores van alle geregistreerde organisaties en voegen deze samen om de basis lijn van **alle organisaties (mediaan)** up-to-date te houden. U kunt het [verzamelen van gegevens](#bkmk_uea_stop) op elk gewenst moment stoppen.

   - Zie [problemen met apparaatregistratie en opstart prestaties oplossen](#bkmk_uea_enrollment_tshooter)voor meer informatie over veelvoorkomende problemen.

## <a name="overview-page"></a>Overzichts pagina

Zodra de gegevens klaar zijn, ziet u een aantal informatie op de pagina **overzicht** , zoals hieronder wordt beschreven:

- De **Score van de gebruikers ervaring** is 50/50 een gewogen gemiddelde van de **Aanbevolen software** -en **prestatie scores**voor het opstarten. We zullen de set subscores in de loop van de tijd uitbreiden.

- U kunt uw huidige Score vergelijken met andere scores door een basis lijn in te stellen.
  - Zoals beschreven in de sectie [basis lijn](#bkmk_uea_baselines) , is er een ingebouwde basis lijn voor een *commerciële mediaan* om te zien hoe u kunt vergelijken met een typische onderneming. U kunt nieuwe basis lijnen maken op basis van uw huidige metrische gegevens, zodat u de voortgang kunt volgen of regressies in de loop van de tijd weer geven.
   - Basislijn markeringen worden weer gegeven voor uw algemene score en subscores. Als een van de scores meer dan de Configureer bare drempel waarde van de geselecteerde basis lijn heeft teruggedraaide, wordt de Score rood weer gegeven en wordt de score op het hoogste niveau gemarkeerd als behoefte aan aandacht.
  - Een status van **onvoldoende gegevens** betekent dat u niet genoeg apparaten rapporteert om een zinvolle score te bieden. Er zijn momenteel ten minste vijf apparaten vereist.

- **Inzichten en aanbevelingen** zijn een lijst met prioriteiten voor het verbeteren van uw score. Deze lijst wordt gefilterd op de context van het subknooppunt wanneer u navigeert naar **Aanbevolen procedures** of **Aanbevolen software**.

[![Overzichts pagina van het eind punt analyse](media/overview-page.png)](media/overview-page.png#lightbox)

## <a name="recommended-software"></a><a name="bkmk_uea_rs"></a>Aanbevolen software

> [!Important]  
> Endpoint Analytics berekent de score voor **Software-acceptatie** voor al uw intune-en gezamenlijk beheerde apparaten, ongeacht of ze zijn geconfigureerd met het [intune-gegevensverzamelings beleid](#bkmk_uea_profile) of niet. Voor door Configuration Manager beheerde apparaten worden scores alleen berekend voor [Inge schreven apparaten](#bkmk_uea_cm_enroll) 

Bepaalde software is bekend bij het verbeteren van de ervaring van de eind gebruiker, onafhankelijk van de status waarden op lagere niveaus. Zo heeft Windows 10 een veel hogere onderpromor score dan Windows 7. De score voor **Software-acceptatie** is een getal tussen 0 en 100 dat een gewogen gemiddelde vertegenwoordigt van het percentage apparaten dat verschillende aanbevolen software heeft geïmplementeerd. De huidige weging is hoger voor Windows dan voor de andere meet gegevens, omdat gebruikers vaker met hen communiceren. De metrische gegevens worden hieronder beschreven: 

[![Pagina met aanbevolen endpoint Analytics-software](media/recommended-software.png)](media/recommended-software.png#lightbox)

### <a name="windows-10"></a><a name="bkmk_uea_win10"></a>Windows 10

Windows 10 biedt een betere gebruikers ervaring dan oudere versies van Windows. Zie het [White Paper Tei](https://vc2prod.blob.core.windows.net/vc-resources/TEIStudies/TEI%20of%20Windows%2010.pdf) voor meer informatie.

Deze metrische waarde meet het percentage apparaten in Windows 10 versus een oudere versie van Windows.

De aanbevolen herstel actie voor het verplaatsen van apparaten uit oudere versies van Windows is het maken van een implementatie plan met [Desktop Analytics](../../desktop-analytics/overview.md).

### <a name="autopilot"></a><a name="bkmk_uea_ap"></a>Auto Pilot

Micro soft auto pilot biedt een eenvoudigere eerste inrichtings ervaring voor Windows 10-Pc's dan de systeem eigen ervaring door het aantal schermen in de out of Box Experience (OOBE) te verminderen en standaard waarden op te geven om ervoor te zorgen dat het apparaat van de werk nemers op de juiste wijze wordt ingericht vanuit de fabriek of bij het opnieuw instellen.

Met deze metrische waarde meet u het percentage Windows 10-apparaten dat is geregistreerd voor auto pilot.

De aanbevolen herstel actie bestaat uit het registreren van bestaande apparaten in auto pilot met behulp van [Microsoft intune](https://docs.microsoft.com/intune/enrollment-autopilot).

### <a name="azure-active-directory"></a><a name="bkmk_uea_aad"></a>Azure Active Directory

Azure Active Directory (Azure AD) biedt gebruikers tal van productiviteits voordelen, waaronder eenmalige aanmelding voor het hele apparaat bij apps en services, aanmelden bij Windows Hello, selfservice BitLocker-herstel en zakelijke gegevens roaming.

Deze metrische waarde meet het percentage apparaten dat is inge schreven in azure AD.

Uw door micro soft intune beheerde apparaten zijn al geregistreerd in azure AD. De aanbevolen herstel actie voor apparaten die worden beheerd door Configuration Manager, is om [ze te registreren in azure AD](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) of [gezamenlijk te beheren](../../comanage/overview.md). Met de co-beheer apparaten wordt ook uw score voor Cloud beheer verbeterd.

### <a name="cloud-management"></a><a name="bkmk_uea_intune"></a>Cloud beheer

Configuration Manager en intune bieden geïntegreerde hulpprogram ma's voor Cloud beheer en unieke opties voor co-beheer voor het inrichten, implementeren, beheren en beveiligen van eind punten en toepassingen in een organisatie. Met de kracht van Cloud Management kunt u diverse productiviteits voordelen bereiken, waaronder het inschakelen van toegang tot bedrijfs bronnen, zelfs wanneer ze zich niet op het bedrijfs netwerk bevinden, en de nood zaak en de prestatie overhead van groepsbeleid elimineren, wat resulteert in een betere ervaring voor de eind gebruiker. 

Met deze metriek wordt het percentage Pc's gemeten dat is gekoppeld aan de Microsoft 365 Cloud om extra mogelijkheden te ontgrendelen. Zie hoe [micro soft dit inschakelt voor onze mede werkers](https://www.microsoft.com/en-us/itshowcase/managing-windows-10-devices-with-microsoft-intune).

De aanbevolen actie voor apparaten die worden beheerd door Configuration Manager die nog niet zijn Inge schreven bij intune, is het [co-beheer](../../comanage/overview.md) voor het ontgrendelen van extra Cloud mogelijkheden zoals voorwaardelijke toegang.

### <a name="no-commercial-median"></a><a name="bkmk_uea_np"></a>Geen bedrijfs mediaan

De ingebouwde basis lijn van de **commerciële mediaan** heeft momenteel geen metrische gegevens voor de subscores die worden vermeld in de bovenstaande secties.

## <a name="startup-performance"></a><a name="bkmk_uea_bp"></a>Opstart prestaties

> [!NOTE]
> Als u geen prestatie gegevens van het opstart proces van al uw apparaten ziet, raadpleegt u [problemen met de registratie van apparaten en opstart prestaties oplossen](#bkmk_uea_enrollment_tshooter).

Met de score voor het opstarten van prestaties kunnen gebruikers snel aan de slag met productiviteit, zonder langdurige opstart-en aanmeldings vertragingen. De **opstart Score** is een getal tussen 0 en 100. Deze score is een gewogen gemiddelde **opstart Score** en de **aanmeldings** Score, die als volgt worden berekend:

- **Opstart Score**: op basis van de tijd van inschakeling om u aan te melden. We kijken naar de laatste opstart tijd van elk apparaat, met uitzonde ring van de update fase en geven vervolgens een Score van 0 (slecht) tot 100 (uitzonderlijk). Deze scores worden gemiddeld voor een algemene opstart score voor de Tenant.
- **Aanmeldings Score**: gebaseerd op de tijd vanaf het moment dat de gebruiker toegang heeft tot een responsieve Desktop (wat betekent dat het bureau blad is gerenderd en het CPU-gebruik gedurende ten minste 2 seconden lager is dan 50%). We kijken naar de laatste aanmeldings tijd op elk apparaat, exclusief de eerste aanmeldingen of aanmeldingen onmiddellijk na een update van de onderdelen, en vervolgens een Score van 0 (slecht) tot 100 (uitzonderlijk). Deze scores worden gemiddeld voor een algemene opstart score voor de Tenant.

[![Start pagina endpoint Analytics-prestaties](media/startup-performance.png)](media/startup-performance.png#lightbox)

### <a name="insights"></a>Inzichten

De pagina **opstart prestaties** biedt ook een overzicht van de **inzichten en aanbevelingen**, zoals beschreven in de volgende secties:

#### <a name="hard-disk-drives"></a><a name="bkmk_uea_hdd"></a>Harde schijven

Opstart prestaties bieden een inzicht in het aantal apparaten waarop de opstart schijf een harde schijf is. Harde schijven hebben doorgaans drie tot vier keer zoveel tijd nodig voor het opstarten van schijven. We rapporteren ook de verwachte verbetering voor het opstarten van prestaties die u zou krijgen door over te stappen op schijven met een Solid-staat.

Klik op dit voor een lijst met apparaten die harde schijven hebben. De aanbevolen actie is om deze apparaten bij te werken naar Solid-State stations.

#### <a name="group-policy"></a><a name="bkmk_uea_gp"></a>groepsbeleid

Opstart prestaties bieden een inzicht in het aantal apparaten dat de opstart-en aanmeldings tijden veroorzaakt door groepsbeleid. Door te klikken, gaat u naar de weer gave apparaten. De weer gave wordt gesorteerd op groepsbeleid tijd, zodat de betrokken apparaten kunnen worden weer gegeven voor verdere probleem oplossing.

Als u op een bepaald apparaat klikt, kunt u de opstart-en aanmeldings geschiedenis bekijken. De geschiedenis helpt u te bepalen of het probleem een regressie is en wanneer deze mogelijk is opgetreden.

Hoewel er veel artikelen zijn over het optimaliseren van de prestaties van groeps beleid, kunt u in plaats daarvan migreren naar Cloud beheer. Door te migreren naar Cloud-beheer kunt u gebruikmaken van [intune-beveiligings basislijnen](https://docs.microsoft.com/intune/protect/security-baselines) en het eerder uitgebrachte beleid analyse programma.

#### <a name="slow-boot-and-sign-in-times"></a><a name="bkmk_uea_sb"></a>Trage opstart-en aanmeldings tijden

Opstart prestaties bieden een inzicht in het aantal apparaten met trage opstarten of aanmeldings tijden. Een opstart Score of een aanmeldings Score van "0" betekent dat het langzaam is. Door te klikken, gaat u naar de weer gave apparaten. De apparaten worden respectievelijk gesorteerd op basis van de kern opstart tijd of de basis tijd van de aanmelding, zodat de betrokken apparaten kunnen worden weer geven voor meer informatie.

Als u op een bepaald apparaat klikt, kunt u de opstart-en aanmeldings geschiedenis bekijken. De geschiedenis helpt u te bepalen of het probleem een regressie is en wanneer deze mogelijk is opgetreden.

### <a name="reporting-tabs"></a>Rapportage tabbladen

De pagina **opstart prestaties** bevat tabbladen met rapporten die ondersteuning bieden voor de inzichten, waaronder:
1. **Model prestaties**. Op dit tabblad ziet u de opstart-en aanmeldings prestaties per model, waarmee u kunt vaststellen of prestatie problemen worden geïsoleerd voor bepaalde modellen.
1. **Prestaties**van het apparaat. Dit tabblad biedt opstart-en aanmeldings gegevens voor al uw apparaten. U kunt sorteren op een bepaalde metrische waarde (bijvoorbeeld een GP-aanmeldings tijd) om te zien welke apparaten de slechtste scores voor die metriek hebben om te helpen bij het oplossen van problemen. U kunt ook op naam zoeken naar een apparaat. Als u via een apparaat klikt, kunt u de opstart-en aanmeldings geschiedenis bekijken, waarmee u kunt nagaan of er een recente regressie is
1. **Opstart processen**. Opstart processen kunnen een negatieve invloed hebben op de gebruikers ervaring door de tijds duur te verhogen die gebruikers nodig hebben om te reageren op het bureau blad. Dit tabblad (indien zichtbaar; we hebben dit alleen naar een of meer van u naar een aantal van u gereisd als we deze functie nog ontwikkelen) laat zien welke processen invloed hebben op de fase van de aanmelding ' tijd voor respons op het bureau blad '; die de CPU boven 50% houdt nadat het bureau blad is gerenderd. De tabel bevat alleen processen die van invloed zijn op een minimum van 10 apparaten in uw Tenant.  

## <a name="proactive-remediations"></a><a name="bkmk_uea_prs"></a>Proactieve herstel bewerkingen

Proactieve herstel bewerkingen zijn script pakketten die veelvoorkomende ondersteunings problemen op het apparaat van een gebruiker kunnen detecteren en oplossen voordat ze zelfs een probleem moeten realiseren. Deze herstel bewerkingen kunnen helpen bij het beperken van ondersteunings aanvragen. U kunt uw eigen script pakket maken of een van de script pakketten implementeren die we hebben geschreven en in onze omgeving gebruiken om ondersteunings tickets te reduceren.

Elk script pakket bestaat uit een detectie script, een herstel script en meta gegevens. Via intune kunt u deze script pakketten implementeren en rapporten op hun doeltreffendheid bekijken. Er worden momenteel nieuwe script pakketten ontwikkeld en u wilt weten hoe u deze kunt gebruiken. Neem contact op met de preview-versie van uw endpoint Analytics als u feedback hebt over de script pakketten.

### <a name="get-the-detection-and-remediation-scripts"></a><a name="bkmk_uea_prs_ps1"></a>De detectie-en herstel scripts ophalen

1. Kopieer de scripts van de onderkant van dit artikel in de sectie [Power shell-scripts](#bkmk_uea_ps_scripts) .
    - Script bestanden waarvan de naam begint met `det` detectie scripts zijn. Herstel scripts beginnen met `rem` .
    - Zie de [script beschrijvingen](#bkmk_uea_scripts)voor een beschrijving van de scripts.
1. Sla elk script op met de gegeven naam. De naam bevindt zich ook in de opmerkingen boven aan elk script.
    - U kunt een andere script naam gebruiken, maar deze komt niet overeen met de naam die wordt vermeld in de sectie [beschrijvingen van scripts](#bkmk_uea_scripts) .


### <a name="deploying-and-monitoring-scripts"></a><a name="bkmk_uea_prs_deploy"></a>Scripts implementeren en bewaken
De **Microsoft intune Management extension** -service haalt de scripts van intune op en voert deze uit. De scripts worden elke 24 uur opnieuw uitgevoerd. Volg de onderstaande instructies om de scripts te implementeren en te controleren:

1. Ga naar het knoop punt **proactieve herstel** bewerkingen in de-console.
1. Klik op de knop **script maken** om een script pakket te maken.
     [![Pagina met proactieve herstel bewerkingen voor endpoint Analytics. Selecteer de koppeling maken.](media/proactive-remediations-create.png)](media/proactive-remediations-create.png#lightbox)
1. Geef in de stap **basis beginselen** een **naam** en optioneel een **Beschrijving**voor het script pakket op. Het veld **Uitgever** kan worden bewerkt, maar wordt standaard ingesteld op de naam van uw Tenant. De **versie** kan niet worden bewerkt. 
1. Kopieer de tekst van de scripts die u hebt gedownload in de velden **detectie script** en **herstel script** van de stap **instellingen** . 
   - U moet het bijbehorende detectie-en herstel script in hetzelfde pakket hebben. Het `Detect_stale_Group_Policies.ps1` detectie script correspondeert bijvoorbeeld met het `Remediate_stale_GroupPolicies.ps1` herstel script.
       [![Pagina met script instellingen voor proactieve herstel bewerkingen voor endpoint Analytics.](media/proactive-remediations-script-settings.png)](media/proactive-remediations-script-settings.png#lightbox)
1. Voltooi de opties op de pagina **instellingen** met de volgende aanbevolen configuraties:
   - **Voer dit script uit met de referenties die zijn aangemeld**: dit is afhankelijk van het script. Zie de [beschrijvingen van scripts](#bkmk_uea_scripts)voor meer informatie.
   - **Handtekening controle van script afdwingen**: Nee
   - **Script uitvoeren in 64-bits Power shell**: Nee
1. Klik op **volgende** en wijs vervolgens de **bereik Tags** toe die u nodig hebt.
1. In de stap **toewijzingen** selecteert u de apparaatgroepen waarvoor u het script pakket wilt implementeren.
1. Voltooi de stap voor het **beoordelen en maken** van uw implementatie.
1. Onder **Reporting**  >  **endpoint Analytics: proactieve herstel**bewerkingen ziet u een overzicht van de status van detectie en herstel.
       [![Overzichts pagina van het rapport met proactieve herstel van eind punten.](media/proactive-remediations-report-overview.png)](media/proactive-remediations-report-overview.png#lightbox)
1. Klik op **Apparaatstatus** om status Details voor elk apparaat in uw implementatie op te halen.
       [![Status van het apparaat voor proactieve herstel bewerkingen voor endpoint Analytics.](media/proactive-remediations-device-status.png)](media/proactive-remediations-device-status.png#lightbox)


## <a name="endpoint-analytics-settings"></a><a name="bkmk_uea_set"></a>Instellingen voor het endpoint Analytics

Op de pagina instellingen kunt u **Algemeen** of **basis lijn**selecteren. Elk van deze instellingen wordt hieronder beschreven:

### <a name="general"></a><a name="bkmk_uea_gen"></a>Algemene

Op de pagina **Algemeen** in **instellingen** kunt u zien of het verzamelen van de gegevens van de intune-opstart prestaties is ingeschakeld. Het wordt automatisch ingeschakeld voor al uw apparaten wanneer u op **starten** klikt om analyse van gebruikers ervaring in te scha kelen. U hebt de optie om naar het knoop punt beleid voor gegevens verzameling van intune te gaan om de set apparaten te wijzigen waarop de opstart-en aanmeldings records worden verzameld.


#### <a name="intune-data-collection-policy"></a><a name="bkmk_uea_profile"></a>Beleid voor verzamelen van intune-gegevens

Als u deze instelling wilt toewijzen aan een subset van apparaten, [maakt u een profiel](/intune/configuration/device-profile-create#create-the-profile) met de volgende gegevens: 

  - **Naam**: Voer een beschrijvende naam in voor het profiel, zoals het beleid voor het **verzamelen van intune-gegevens**
   
  - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.
    
  - **Platform**: Selecteer **Windows 10 en hoger**
   
  - **Profiel type**: Selecteer **Windows status controle**
   
  - Configureer de **instellingen**:
   
       - **Status controle**: Selecteer **inschakelen** om gebeurtenis gegevens van Windows 10-apparaten te verzamelen
    
    - **Bereik**: **opstart prestaties** selecteren 

  - Gebruik de regels voor [bereik Tags](/intune/configuration/device-profile-create#scope-tags) en [toepasselijkheid](/intune/configuration/device-profile-create#applicability-rules) om het profiel te filteren op specifieke IT-groepen of apparaten in een groep die aan een bepaald criterium voldoen.

> [!NOTE]
> Er is een tijdelijke aanduiding voor instructies voor het configureren van de Configuration Manager Data Connector. Deze functionaliteit is echter niet geïmplementeerd in deze eerste persoonlijke preview.

  [![Pagina met algemene instellingen voor endpoint Analytics](media/settings-general.png)](media/settings-general.png#lightbox)

### <a name="baseline-management"></a><a name="bkmk_uea_baselines"></a>Basislijn beheer

Met een basis lijn kunt u uw huidige scores en subscores vergelijken met anderen.

1. Er is een ingebouwde basis lijn voor **commerciële mediaan**, waarmee u uw scores kunt vergelijken met een typische onderneming.
1. U kunt nieuwe basis lijnen maken op basis van uw huidige metrische gegevens om de voortgang bij te houden of om regressies in de loop van de tijd weer te geven. Klik op de knop **nieuwe maken** en geef de nieuwe basis lijn een naam. We raden u aan een naam op te nemen die de datum bevat, zodat u deze gemakkelijker kunt selecteren in de vervolg keuzelijst in de rapport pagina's.
1. Er is een limiet van 100 basis lijnen per Tenant. U kunt oude basis lijnen verwijderen die niet meer nodig zijn.
1. Uw huidige metrische gegevens worden gemarkeerd als rood en worden weer gegeven als teruggedraaide als ze onder de huidige basis lijn in uw rapporten vallen. Omdat de metrische gegevens van dag tot dag kunnen worden geschommeld, kunt u een regressie drempel instellen, die standaard wordt ingesteld op 10%. Met deze drempel waarde worden metrische gegevens alleen als teruggedraaide gemarkeerd als ze met meer dan 10% zijn teruggedraaide.

   [![Pagina instellingen voor endpoint Analytics-basis](media/settings-baseline.png)](media/settings-baseline.png#lightbox)

## <a name="troubleshooting"></a><a name="bkmk_uea_tshoot"></a>Meer

De onderstaande secties kunnen worden gebruikt voor het oplossen van problemen die kunnen optreden.

### <a name="troubleshooting-device-enrollment-and-startup-performance"></a><a name="bkmk_uea_enrollment_tshooter"></a>Problemen met de registratie van apparaten en opstart prestaties oplossen

Als op de pagina overzicht een prestatie Score van nul wordt weer gegeven, vergezeld van een banner met de melding dat deze op gegevens wordt gewacht, of als het tabblad prestaties van opstart prestaties van apparaat minder apparaten bevat dan u verwacht, zijn er enkele stappen die u kunt ondernemen om het probleem op te lossen.

Zorg er eerst voor dat apparaten voldoen aan de [technische vereisten](#technical-prerequisites)

Voor intune-of gezamenlijk beheerde apparaten die zijn geconfigureerd met het intune-beleid voor gegevens verzameling:
1. Zorg ervoor dat het beleid voor het [verzamelen van intune-gegevens](#bkmk_uea_profile) is gericht op alle apparaten waarvoor u prestatie gegevens wilt bekijken. Ga naar het tabblad toewijzing om te controleren of deze is toegewezen aan de verwachte set apparaten. 
1. Zoek naar apparaten die niet met succes zijn geconfigureerd voor het verzamelen van gegevens. U kunt deze informatie ook bekijken op de pagina overzicht van profielen.  
   - Er is een bekend probleem waarbij klanten profiel toewijzings fouten kunnen zien, waarbij de betrokken apparaten een fout code van weer geven `-2016281112 (Remediation failed)` . Dit probleem wordt momenteel onderzocht.
1. Apparaten die zijn geconfigureerd voor het verzamelen van gegevens moeten opnieuw worden gestart nadat het verzamelen van gegevens is ingeschakeld en u moet vervolgens tot 25 uur wachten totdat het apparaat wordt weer gegeven op het tabblad prestaties van apparaat. [Gegevens stroom](#data-flow) weer geven
1. Als uw apparaat is geconfigureerd voor het verzamelen van gegevens, vervolgens opnieuw is gestart en u deze 25 uur nog niet ziet, is het mogelijk dat het apparaat niet kan communiceren met de vereiste eind punten. Zie [proxy configuratie](#bkmk_uea_endpoints).

Voor door Configuration Manager beheerde apparaten:
1. Zorg ervoor dat alle apparaten die u wilt weer geven de prestatie gegevens zijn [Inge schreven](#bkmk_uea_cm_enroll)
1. Controleer of de gegevens die worden geüpload van Configuration Manager naar de Gateway Service zijn geslaagd door te kijken naar de fout berichten in het bestand **UXAnalyticsUploadWorker. log** op de site server.
1. Controleer of een beheerder aangepaste onderdrukkingen voor client instellingen heeft.  Ga in de Configuration Manager-console naar de werk ruimte **apparaten** , zoek de doel apparaten en selecteer de **resulterende client instellingen**in de groep **client instellingen** . Als endpoint Analytics is uitgeschakeld, worden de client instellingen genegeerd. De client instellingen overschrijven en endpoint Analytics hierop inschakelen.  
1. Controleer of ontbrekende client apparaten gegevens verzenden naar de site server door het bestand **SensorEndpoint. log** te bekijken `C:\Windows\CCM\Logs\` op client apparaten. Zoeken naar berichten die zijn *verzonden* .
1. Controleer en los eventuele fouten ocurring tijdens de verwerking van de opstart gebeurtenissen op door het bestand **SensorManagedProvider. log** te bekijken `C:\Windows\CCM\Logs\` op client apparaten.


### <a name="proxy-configuration"></a><a name="bkmk_uea_endpoints"></a>Proxy configuratie

Als uw omgeving een proxy server gebruikt, configureert u de proxy server zo dat de volgende eind punten zijn toegestaan:

#### <a name="endpoints-required-for-configuration-manager-managed-devices"></a>Vereiste eind punten voor door Configuration Manager beheerde apparaten

Configuration Manager-beheerde apparaten verzenden gegevens naar intune via de connector van de Configuration Manager-rol en hebben geen rechtstreekse toegang tot de open bare cloud van micro soft.

| Eindpunt  | Functie  |
|-----------|-----------|
| `https://graph.windows.net` | Wordt gebruikt om automatisch instellingen op te halen wanneer u uw hiërarchie koppelt aan endpoint Analytics op Configuration Manager serverrol. Zie [Configure the proxy for a site System server](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)(Engelstalig) voor meer informatie. |
| `https://*.manage.microsoft.com` | Wordt gebruikt voor het synchroniseren van apparaten verzameling en apparaten met endpoint Analytics op Configuration Manager server functie. Zie [Configure the proxy for a site System server](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)(Engelstalig) voor meer informatie. |

#### <a name="endpoints-required-for-intune-managed-devices"></a>Vereiste eind punten voor door intune beheerde apparaten

Als u apparaten wilt registreren bij Endpoint Analytics, moeten ze de vereiste functionele gegevens verzenden naar de open bare cloud van micro soft. Endpoint Analytics maakt gebruik van Windows 10 en Windows Server verbonden gebruikers ervaringen en telemetrie-onderdelen (DiagTrack) voor het verzamelen van de gegevens van door intune beheerde apparaten. Zorg ervoor dat de **verbonden gebruikers ervaring en telemetrie** -service op het apparaat wordt uitgevoerd.

| Eindpunt  | Functie  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Wordt gebruikt door door intune beheerde apparaten om [vereiste functionele gegevens](#bkmk_uea_datacollection) te verzenden naar het eind punt van de intune-gegevens verzameling. |

> [!Important]  
> Voor privacy-en gegevens integriteit controleert Windows naar een micro soft SSL-certificaat (certificaat vastmaken) bij het communiceren met de vereiste eind punten voor het delen van gegevens. SSL-onderscheping en-inspectie zijn niet mogelijk. Als u endpoint Analytics wilt gebruiken, moet u deze eind punten uitsluiten van SSL-inspectie.<!-- BUG 4647542 -->

##### <a name="proxy-server-authentication"></a>Verificatie van de proxy server

Als uw organisatie verificatie van de proxy server gebruikt voor Internet toegang, moet u ervoor zorgen dat de gegevens niet worden geblokkeerd vanwege de verificatie. Als uw proxy niet toestaat dat apparaten deze gegevens verzenden, worden ze niet weer gegeven in Desktop Analytics.

##### <a name="bypass-recommended"></a>Bypass (aanbevolen)

Configureer uw proxy servers zo dat er geen proxy verificatie nodig is voor het verkeer naar de eind punten voor het delen van gegevens. Deze optie is de meest uitgebreide oplossing. Het werkt voor alle versies van Windows 10.  

##### <a name="user-proxy-authentication"></a>Verificatie van de gebruikers proxy

Apparaten configureren voor het gebruik van de context van de aangemelde gebruiker voor proxy verificatie. Voor deze methode zijn de volgende configuraties vereist:

- Apparaten hebben de huidige kwaliteits update voor een ondersteunde versie van Windows

- Configureer proxy op gebruikers niveau (WinINET-proxy) in **proxy-instellingen** in het netwerk & Internet groep Windows-instellingen. U kunt ook de verouderde Internet opties in het configuratie scherm gebruiken.

- Zorg ervoor dat de gebruikers over proxy machtigingen beschikken om de eind punten voor het delen van gegevens te bereiken. Deze optie vereist dat de apparaten console gebruikers hebben met proxy machtigingen, zodat u deze methode niet kunt gebruiken met headless apparaten.

> [!IMPORTANT]
> De verificatie methode voor de gebruikers proxy is niet compatibel met het gebruik van micro soft Defender Advanced Threat Protection. Dit gedrag is omdat deze verificatie afhankelijk is van de **DisableEnterpriseAuthProxy** -register sleutel die is ingesteld op `0` , terwijl micro soft Defender ATP vereist dat deze is ingesteld op `1` . Zie [instellingen voor machine proxy en Internet connectiviteit configureren in micro soft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection)voor meer informatie.

##### <a name="device-proxy-authentication"></a>Verificatie van Device proxy

Deze aanpak ondersteunt de volgende scenario's:

- Headless apparaten, waar geen gebruiker zich aanmeldt of gebruikers van het apparaat hebben geen toegang tot Internet

- Geverifieerde proxy's die geen geïntegreerde Windows-verificatie gebruiken

- Als u ook micro soft Defender Advanced Threat Protection gebruikt

Deze benadering is het meest gecompliceerd omdat hiervoor de volgende configuraties zijn vereist:

- Zorg ervoor dat apparaten de proxy server kunnen bereiken via WinHTTP in de context van het lokale systeem. Gebruik een van de volgende opties om dit gedrag te configureren:

  - De opdracht regel`netsh winhttp set proxy`

  - WPAD-protocol (Web Proxy Auto-Discovery)

  - Transparante proxy

  - WinINET-proxy voor het hele apparaat configureren met de volgende groeps beleids instelling: **proxy-instellingen per computer (in plaats van per gebruiker) maken** (ProxySettingsPerUser = `1` )

  - Gerouteerde verbinding of die gebruikmaakt van Network Address Translation (NAT)

- Configureer proxy servers zodanig dat de computer accounts in Active Directory toegang hebben tot de gegevens eindpunten. Voor deze configuratie zijn proxy servers vereist voor ondersteuning van geïntegreerde Windows-authenticatie.  


## <a name="frequently-asked-questions"></a><a name="bkmk_uea_faq"></a>Veelgestelde vragen

### <a name="will-my-endpoint-analytics-data-migrate-if-i-move-my-intune-tenant-to-a-different-tenant-location"></a>Worden mijn endpoint Analytics-gegevens gemigreerd als ik mijn intune-Tenant naar een andere Tenant locatie Verplaats?

Als u uw intune-Tenant naar een andere locatie migreert, gaan alle gegevens in uw endpoint Analytics-oplossing op het moment van de migratie verloren. Omdat de eind punten in endpoint Analytics voortdurend in het rapport staan, worden alle gebeurtenissen die na de migratie worden uitgevoerd, automatisch naar uw nieuwe Tenant locatie en rapporten geuploadd, ervan uitgaande dat apparaten op de juiste wijze zijn Inge schreven. 

### <a name="why-are-the-scripts-exiting-with-a-code-of-1"></a>Waarom worden de scripts afgesloten met de code 1?

De scripts worden afgesloten met een code van 1 om aan te geven dat het herstel moet worden uitgevoerd door intune. In dit geval moet u een detectie Script afsluiten met 1, het is waar het herstellen nodig is. Veel script pakketten die alleen in CM worden uitgevoerd, kunnen voldoen aan het beleid, maar sluiten met een code van 1. Voor deze scripts wordt het afsluiten met een code van 1 niet iets van een alarm, maar u kunt ook controleren of het apparaat correct is hersteld.

### <a name="why-did-the-update-stale-group-policies-script-return-with-error-0x87d00321"></a>Waarom is het script voor het bijwerken van verouderde groeps beleidsregels geretourneerd met fout 0x87D00321?

0x87D00321 is een time-outfout voor het uitvoeren van scripts. Deze fout treedt meestal op bij computers die extern zijn verbonden. Een mogelijke beperking is dat u alleen kunt implementeren naar een dynamische verzameling machines die een interne netwerk verbinding hebben.

## <a name="script-descriptions"></a><a name="bkmk_uea_scripts"></a>Script beschrijvingen

In deze tabel worden de script namen, beschrijvingen, detecties, herstel bewerkingen en configureer bare items weer gegeven. Script bestanden waarvan de naam begint met `Detect` detectie scripts zijn. Herstel scripts beginnen met `Remediate` . Deze scripts kunnen worden gekopieerd uit de volgende sectie in dit artikel.

|Scriptnaam|Beschrijving|
|---|---|
|**Verlopen groeps beleid bijwerken** </br>`Detect_stale_Group_Policies.ps1` </br> `Remediate_stale_GroupPolicies.ps1`| Detecteert of de laatste groepsbeleid vernieuwing groter is dan `7 days` geleden.  </br>Pas de drempel van 7 dagen aan door de waarde voor `$numDays` in het detectie script te wijzigen. </br></br>Opgelost door uit te voeren `gpupdate /target:computer /force` en`gpupdate /target:user /force`  </br> </br>Kan helpen bij het verminderen van ondersteuning bij netwerk connectiviteit wanneer certificaten en configuraties via groepsbeleid worden geleverd. </br> </br> **Voer het script uit met de referenties die zijn aangemeld**: Ja|
|**Office klik-en-klaar-service opnieuw starten** </br> `Detect_Click_To_Run_Service_State.ps1` </br> `Remediate_Click_To_Run_Service_State.ps1`| Detecteert of de klik-en-klaar-service is ingesteld op automatisch starten en als de service wordt gestopt. </br> </br> Herstel door de service zodanig in te stellen dat deze automatisch wordt gestart en de service wordt gestart als deze is gestopt. </br></br> Helpt problemen op te lossen waarbij Win32-Microsoft 365-apps voor bedrijven niet starten omdat de klik-en-klaar-service is gestopt. </br> </br> **Voer het script uit met de referenties die zijn aangemeld**: Nee|
|**Controleer netwerk certificaten** </br>`Detect_Expired_Issuer_Certificates.ps1` </br>`Remediate_Expired_Issuer_Certificates.ps1`|Hiermee worden certificaten gedetecteerd die zijn uitgegeven door een certificerings instantie in het persoonlijke archief van de computer of gebruiker die verlopen of bijna verlopen zijn. </br> Geef de CA op door de waarde voor `$strMatch` in het detectie script te wijzigen. Geef 0 op `$expiringDays` om verlopen certificaten te vinden of geef een ander aantal dagen op om certificaten bij verval datum te vinden.  </br></br>Herstel door een pop-upmelding naar de gebruiker te verhogen. </br> Geef de `$Title` waarden en op `$msgText` bij de titel van het bericht en de tekst die gebruikers moeten zien. </br> </br> Hiermee worden gebruikers op de hoogte gesteld van verlopen certificaten die mogelijk moeten worden vernieuwd. </br> </br> **Voer het script uit met de referenties die zijn aangemeld**: Nee|
|**Verouderde certificaten wissen** </br>`Detect_Expired_User_Certificates.ps1` </br> `Remediate_Expired_User_Certificates.ps1`| Hiermee worden verlopen certificaten gedetecteerd die zijn uitgegeven door een certificerings instantie in het persoonlijke archief van de huidige gebruiker. </br> Geef de CA op door de waarde voor `$certCN` in het detectie script te wijzigen. </br> </br> Herstel door verlopen certificaten te verwijderen die zijn uitgegeven door een certificerings instantie uit het persoonlijke archief van de huidige gebruiker. </br> Geef de CA op door de waarde voor `$certCN` in het herstel script te wijzigen. </br> </br> Hiermee worden verlopen certificaten die zijn uitgegeven door een CA uit het persoonlijke archief van de huidige gebruiker gevonden en verwijderd. </br> </br> **Voer het script uit met de referenties die zijn aangemeld**: Ja|

## <a name="powershell-scripts"></a><a name="bkmk_uea_ps_scripts"></a>Power shell-scripts

### <a name="detect_stale_group_policiesps1"></a>Detect_stale_Group_Policies.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_stale_Group_Policies.ps1
# Description:     Detect if Group Policy has been updated within number of days
# Notes:           Remediate if "Match", $numDays default value of 7, change as appropriate
#
#=============================================================================================================================

# Define Variables
$numDays = 7

try {
    $gpResult = gpresult /R | Select-String -pattern "Last time Group Policy was applied:" | Select-Object -last 1

    if ($gpResult){
    [int]$lastGPUpdateDays = (New-TimeSpan -Start $lastGPUpdateDate -End (Get-Date)).Days
        if ($lastGPUpdateDays -gt $numDays){
            #We want within last $numDays so we get "Match"
            Write-Host "Match"
            exit 1
        }
        else {
            #Script succeeds but > $numDays since last update so remediate
            #Exit 1 for Intune and "Match" for ConfigMan
            Write-Host "No_Match"
            exit 0
        }
    }
}
catch {
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_stale_grouppoliciesps1"></a>Remediate_stale_GroupPolicies.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_stale_GroupPolicies.ps1
# Description:     This script triggers Group Policy update
# Notes:           No variable substitution needed
#
#=============================================================================================================================

try{
    $compGP = gpupdate /target:computer /force | out-string
    $userGP = gpupdate /target:user /force | out-string
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="detect_click_to_run_service_stateps1"></a>Detect_Click_To_Run_Service_State.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Click_To_Run_Service_State.ps1
# Description:     Detect if Office 16 installed and if "Click to Run Service" is running.
# Notes:           No variable substitution should be necessary
#
#=============================================================================================================================

# Define Variables
$curSvcStat,$svcCTRSvc,$errMsg = "","",""

# Main script
If (-not (Test-Path -Path 'hklm:\Software\Microsoft\Office\16.0')){
    Return "Office 16.0 (or greater) not present on this machine"
    exit 0   
} 

Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
}

Catch{    
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}

If ($curSvcStat -eq "Running"){
    Write-Output $curSvcStat
    exit 0                        
}
Else{
    If($curSvcStat -eq "Stopped"){
    Write-Output $curSvcStat
    exit 1     
    }
}
Else{
    Write-Error "Error: " + $errMsg
    exit 1
}
```

### <a name="remediate_click_to_run_service_stateps1"></a>Remediate_Click_To_Run_Service_State.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Click_To_Run_Service_State.ps1
# Description:     Start the "Click to Run Service" and change its startup type to Automatic
#       Notes:     No variable substitution needed
#
#=============================================================================================================================

# Define Variables
$svcCur = "ClickToRunSvc"
$curSvcStat,$svcCTRSvc,$errMsg = "","",""
$ctr = 0

# Main script
# Make sure nothing has changed since detection, the service exists and is stopped
Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
    }

Catch{    
    $errMsg = $_.Exception.Message
    }
        
# If the service got started between detection and now (nested if) then return
# If the service got uninstalled or corrupted between detection and now (else) then return the "Error: " + the error
If ($curSvcStat -ne "Stopped"){
    If ($curSvcStat -eq "Running"){
        return
    }
    Else{
        return "Error: " + $errMsg
    }
}

# Service should be there and stopped, change the startup type and start
Try{        
    Set-Service $svcCur -StartupType Automatic
    Start-Service $svcCur
    $svcCTRSvc = Get-Service $svcCur
    $curSvcStat = $svcCTRSvc.Status
        While ($curSvcStat.Equals("Stopped")){
            Start-Sleep -Seconds 5
            ctr++
            if(ctr == 12){
                Return "Service could not be started after 60 seconds"
                break
            }
        }
    }

Catch{    
    $errMsg = $_.Exception.Message
    Return $errMsg
    }

Return $curSvcStat
```

### <a name="detect_expired_issuer_certificatesps1"></a>Detect_Expired_Issuer_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_Issuer_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" in either Machine
#                  or User certificate store
# Notes:           Change the value of the variable $strMatch from "CN=<your CA here>" to "CN=..."
#                  For testing purposes the value of the variable $expiringDays can be changed to a positive integer
#                  Don't change the $results variable
#
#=============================================================================================================================

# Define Variables
$results = @()
$expiringDays = 0
$strMatch = "CN=<your CA here>"

try
{
    $results = @(Get-ChildItem -Path Cert:\LocalMachine\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch})
    $results += @(Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch}) 
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        #No matching certificates, do not remediate
        Write-Host "No_Match"        
        exit 0
    }   
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_issuer_certificatesps1"></a>Remediate_Expired_Issuer_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_Issuer_Certificates.ps1
# Description:     Raise a Toast Notification if expired certificates issued by "CN=..."
#                  to user or machine on the machine where detection script found them. No remediation action besides
#                  the Toast is taken.
# Notes:           Change the values of the variables $Title and $msgText
#
#=============================================================================================================================

## Raise toast to have user contact whoever is specified in the $msgText

# Define Variables
$delExpCert = 0
$Title = "Title"
$msgText = "message"

# Main script
[Windows.UI.Notifications.ToastNotificationManager, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.UI.Notifications.ToastNotification, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.Data.Xml.Dom.XmlDocument, Windows.Data.Xml.Dom.XmlDocument, ContentType = WindowsRuntime] | Out-Null

$APP_ID = '{1AC14E77-02E7-4E5D-B744-2EB1AE5198B7}\WindowsPowerShell\v1.0\powershell.exe'

$template = @"
<toast>
    <visual>
        <binding template="ToastText02">
            <text id="1">$Title</text>
            <text id="2">$msgText</text>
        </binding>
    </visual>
</toast>
"@

$xml = New-Object Windows.Data.Xml.Dom.XmlDocument
$xml.LoadXml($template)
$toast = New-Object Windows.UI.Notifications.ToastNotification $xml
[Windows.UI.Notifications.ToastNotificationManager]::CreateToastNotifier($APP_ID).Show($toast)
```

### <a name="detect_expired_user_certificatesps1"></a>Detect_Expired_User_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_User_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=...".
#                  Don't change $results
#
#=============================================================================================================================

# Define Variables
$results = 0
$certCN = "CN=<your CA here>"

try
{   
    $results = Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)}
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        Write-Host "No_Match"
        exit 0
    }    
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_user_certificatesps1"></a>Remediate_Expired_User_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_User_Certificates.ps1
# Description:     Remove expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=..."
#
#=============================================================================================================================

# Define Variables
$certCN = "CN=<your CA here>"

try
{
    Get-ChildItem -Path cert:\CurrentUser -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)} | Remove-Item
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

## <a name="endpoint-analytics-data-privacy"></a><a name="bkmk_uea_privacy"></a>Gegevens privacy voor endpoint Analytics

### <a name="data-flow"></a>Gegevensstroom

In de volgende afbeelding ziet u hoe vereiste functionele gegevens stromen van afzonderlijke apparaten via onze gegevens Services, tijdelijke opslag en uw Tenant. 

[![Diagram voor gegevens stroom van gebruikers ervaring](media/endpoint-analytics-dataflow.png)](media/endpoint-analytics-dataflow.png#lightbox)

1. De [rol van de intune-service beheerder](../../../intune/fundamentals/role-based-access-control.md) [begint](#bkmk_uea_start)met het verzamelen van gegevens.

    - Voor apparaten die door intune worden beheerd, wordt met deze stap het intune-beleid voor **gegevens verzameling** geconfigureerd. Dit beleid wordt standaard toegewezen aan alle apparaten. U kunt [de toewijzing](#bkmk_uea_set) op elk gewenst moment wijzigen in een subset van apparaten of helemaal geen apparaten.

    - Schakel voor door Configuration Manager beheerde apparaten [endpoint Analytics-gegevens verzameling en registratie van apparaten](#bkmk_uea_cm_enroll)in.

1. Apparaten verzenden vereiste functionele gegevens.

    - Voor intune-en gezamenlijk beheerde apparaten met het toegewezen beleid, hebben apparaten rechtstreeks functionele gegevens nodig voor de micro soft endpoint Management-service in de open bare cloud van micro soft, waar in bijna realtime wordt verwerkt. Zie voor meer informatie [vereiste eind punten voor door intune beheerde apparaten](#bkmk_uea_endpoints).

    - Voor door Configuration Manager beheerde apparaten worden gegevens naar micro soft-eindpunt beheer geleid via de ConfigMgr-connector. Apparaten hebben geen directe toegang tot de open bare cloud van micro soft nodig, maar de ConfigMgr-connector is verbonden met de Cloud en vereist een verbinding met een intune-Tenant. Apparaten verzenden elke 24 uur gegevens naar de Configuration Manager-server functie en de Configuration Manager-connector stuurt elk uur gegevens naar de Gateway Service.

1. De micro soft endpoint Management-service verwerkt gegevens voor elk apparaat en publiceert de resultaten voor zowel afzonderlijke apparaten als organisatie aggregaten in de beheer console met behulp van MS Graph Api's. De maximale latentie end-to-end is 25 uur en wordt gegatedeerd op de tijd die nodig is om de dagelijkse verwerking van inzichten en aanbevelingen uit te voeren.

> [!Note]  
> Wanneer u endpoint Analytics voor het eerst [inschakelt](../../tenant-attach/device-sync-actions.md#enable-device-upload) , nieuwe clients toevoegt aan het beleid voor het [verzamelen van intune-gegevens](#bkmk_uea_profile), of het uploaden van apparaten voor een nieuwe verzameling mogelijk maakt, worden in de rapporten in de Endpoint Analytics-Portal niet de volledige gegevens meteen weer gegeven. De gegevens die nodig zijn voor het berekenen van de opstart score voor een apparaat, worden tijdens de opstart tijd gegenereerd. Afhankelijk van de energie-instellingen en gebruikers gedrag kan het weken duren nadat een apparaat is inge schreven om de opstart Score weer te geven op de beheer console.

### <a name="data-collection"></a><a name="bkmk_uea_datacollection"></a>Gegevensverzameling

Momenteel verzamelt de basis functionaliteit van endpoint Analytics informatie die is gekoppeld aan opstart prestatie records die in de [geïdentificeerde](../../../intune/protect/privacy-data-collect.md#identified-data) en [gepseudoniemde](../../../intune/protect/privacy-data-collect.md#pseudonymized-data) categorieën vallen. Wanneer we meer functionaliteit gedurende een bepaalde periode toevoegen, worden de verzamelde gegevens zo nodig verschillend. Het belangrijkste data Points dat momenteel wordt verzameld:

#### <a name="identified-data"></a>Geïdentificeerde gegevens

- Hardware-inventarisatiegegevens
  - **maken:** Fabrikant van apparaat
  - **model:** Model apparaat
  - **deviceClass:** De classificatie van het apparaat. Bijvoorbeeld Desktop, server of mobiel.
  - **Land:** De instelling voor de regio van het apparaat
- Toepassingsinventaris, zoals
  - **naam:** Windows
  - **ver:** De versie van het huidige besturings systeem.
  
#### <a name="pseudonymized-data"></a>Gepseudonimiseerde gegevens

- Diagnostische gegevens, prestatiegegevens en gebruiksgegevens die zijn gekoppeld aan een gebruiker en/of apparaat
  - **logOnId**
  - **opstartid:** De opstart-ID van het systeem
  - **coreBootTimeInMilliseconds:** Tijd voor kern opstarten
  - **totalBootTimeInMilliseconds:** Totale opstart tijd
  - **updateTimeInMilliseconds:** Tijdstip waarop de besturingssysteem updates zijn voltooid
  - **gpLogonDurationInMilliseconds**: tijd voor het verwerken van groeps beleid
  - **desktopShownDurationInMilliseconds:** De tijd voor het laden van bureau blad (explorer.exe)
  - **desktopUsableDurationInMilliseconds:** De tijd voor het bureau blad (explorer.exe) kan alleen worden gebruikt
  - **topProcesses:** Lijst met processen die tijdens het opstarten worden geladen met de naam, met statistieken voor CPU-gebruik en app-Details (naam, uitgever, versie). Bijvoorbeeld *{ \" verwerker \" : \" svchost \" , \" CpuUsage \" : 43, \" ProcessFullPath \" : \" C: \\ \\ Windows \\ \\ System32 \\ \\svchost.exe\" , \" ProductName \" : \" micro soft &reg; Windows- &reg; besturings systeem \" , \" Uitgever \" : \" micro soft Corporation \" , \" productVersion \" : \" 10.0.18362.1 \" }*
- Gegevens van apparaten die niet zijn gekoppeld aan een apparaat of gebruiker (als deze gegevens zijn gekoppeld aan een apparaat of gebruiker, worden deze gegevens behandeld als geïdentificeerde gegevens)
  - **Id:** Unieke apparaat-ID die wordt gebruikt door Windows Update
  - **localId:** Een lokaal gedefinieerde unieke ID voor het apparaat. Dit is niet de door de mens lees bare apparaatnaam. Waarschijnlijk gelijk aan de waarde die is opgeslagen op HKLM\Software\Microsoft\SQMClient\MachineId.
  - **aaddeviceid:** Azure Active Directory apparaat-ID
  - **orgId:** Unieke GUID die de micro soft O365-Tenant vertegenwoordigt
  
> [!Important]  
> Ons beleid voor gegevens verwerking wordt beschreven in de [privacyverklaring van Microsoft intune](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement). We gebruiken alleen uw klant gegevens om u de services te bieden die u hebt geregistreerd voor. Zoals beschreven tijdens het voorbereidings proces, kunnen we de scores van alle geregistreerde organisaties anoniem makeneren en samen voegen om de basis lijn van **alle organisaties (mediaan)** up-to-date te houden.

### <a name="stop-gathering-data"></a><a name="bkmk_uea_stop"></a>Geen gegevens meer verzamelen

- Als u alleen door intune beheerde apparaten wilt inschrijven, verwijdert u het [intune-gegevensverzamelings beleid](#bkmk_uea_gen) dat is gemaakt tijdens de registratie.

- Als u apparaten registreert die worden beheerd door Configuration Manager, moet u de volgende stappen uitvoeren om het uploaden van gegevens in Configuration Manager uit te scha kelen:

   1. Ga in de Configuration Manager-console naar **beheer**  >  **Cloud Services**  >  **co-beheer**.
   1. Selecteer **CoMgmtSettingsProd** en klik vervolgens op **Eigenschappen**.
   1. Schakel op het tabblad **Upload configureren** de optie uit om **endpoint Analytics in te scha kelen voor apparaten die zijn geüpload naar micro soft Endpoint Manager**.

- Gegevens verzameling voor endpoint Analytics in Configuration Manager uitschakelen (optioneel):

   1. Ga in de Configuration Manager-console naar de client instellingen voor de **beheerders**  >  **Client Settings**  >  **instelling**.
   1. Klik met de rechter muisknop en selecteer **Eigenschappen** en selecteer vervolgens de instellingen van de **computer agent** .
   1. Stel **endpoint Analytics-gegevens verzameling** in op **Nee**.
   > [!Important]
   > Als u een bestaande aangepaste client agent hebt ingesteld die op uw apparaten is geïmplementeerd, moet u de optie voor het **verzamelen van endpoint Analytics-gegevens** in deze aangepaste instelling bijwerken en vervolgens opnieuw implementeren op uw computers om deze van kracht te laten worden.

### <a name="resources"></a>Resources

Raadpleeg de volgende artikelen voor meer informatie over verwante privacy-aspecten:

- [Privacyverklaring van Microsoft Intune](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement)
- [Naleving van Windows 10 en privacy](https://docs.microsoft.com/windows/privacy/windows-10-and-privacy-compliance)
- [Licentie voorwaarden en documentatie](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  
- [Beveiliging en privacy op Microsoft Azure data centers](https://azure.microsoft.com/global-infrastructure/)  
- [Vertrouwen in de vertrouwde Cloud](https://azure.microsoft.com/overview/trusted-cloud/)  
- [Vertrouwenscentrum](https://www.microsoft.com/trustcenter)  
