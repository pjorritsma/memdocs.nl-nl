---
title: Asset Intelligence-Inleiding
titleSuffix: Configuration Manager
description: Gebruik Asset Intelligence in Configuration Manager om het gebruik van software licenties in uw onderneming te inventariseren en te beheren.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 25deb098f6e1f4ce275a0c0a0817249cd36558f7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714183"
---
# <a name="introduction-to-asset-intelligence-in-configuration-manager"></a>Inleiding tot Asset Intelligence in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Inventariseer en beheer software licentie gebruik in uw hele onderneming met behulp van de Asset Intelligence-catalogus. Asset Intelligence voegt hardware-inventaris klassen toe om de omvang van de gegevens die Configuration Manager verzamelt, te verbeteren. Deze informatie omvat de hardware-en software titels die in uw omgeving worden gebruikt. Meer dan 60 rapporten bevatten deze informatie in een gemakkelijk te gebruiken indeling. Veel van deze rapporten zijn gekoppeld aan meer specifieke rapporten. Query's uitvoeren voor algemene informatie en inzoomen op meer gedetailleerde informatie. 

Aangepaste gegevens toevoegen aan de Asset Intelligence-catalogus. Bijvoorbeeld aangepaste software categorieën, software families, software-etiketten en hardwarevereisten. Om de Asset Intelligence-catalogus dynamisch bij te werken met de meest recente beschik bare informatie, verbindt u deze met de Microsoft Cloud. 

Gebruik Asset Intelligence voor het afstemmen van het gebruik van uw Enter prise-software licentie. Software licentie gegevens importeren in de site database van Configuration Manager om deze weer te geven voor de software die wordt gebruikt.  



## <a name="asset-intelligence-catalog"></a><a name="BKMK_AssetIntelligenceCatalog"></a>Asset Intelligence-catalogus  

De Asset Intelligence-catalogus is een set database tabellen die zijn opgeslagen in de site database. Deze tabellen bevatten categorisatie-en identificatie gegevens voor meer dan 300.000 software titels en-versies. Ze helpen ook de hardwarevereisten voor specifieke software titels te beheren.  

Asset Intelligence bevat software licentie-informatie voor software titels die worden gebruikt, zowel van micro soft als van andere software van micro soft. Een vooraf gedefinieerde set hardwarevereisten voor software titels is beschikbaar in de Asset Intelligence-catalogus en u kunt nieuwe door de gebruiker gedefinieerde hardwarevereisten maken om te voldoen aan aangepaste vereisten. U kunt ook informatie in de Asset Intelligence-catalogus aanpassen en u kunt informatie over software titels uploaden naar de micro soft-Cloud voor categorisatie.  

Asset Intelligence-catalogus updates die nieuw uitgebrachte software bevatten, zijn periodiek beschikbaar om te worden gedownload voor het uitvoeren van bulksgewijs catalogus updates. Het kan ook dynamisch worden bijgewerkt met behulp van het Asset Intelligence-synchronisatie punt.  


### <a name="software-categories"></a><a name="BKMK_SoftwareCategories"></a>Software categorieën  

Asset Intelligence-software categorieën worden gebruikt om geïnventariseerde software titels te categoriseren en als groeperingen op hoog niveau van specifieke software families. Een mogelijke softwarecategorie is bijvoorbeeld energiebedrijven en een softwarefamilie binnen deze softwarecategorie kan olie en gas of hydro-elektrisch zijn. Veel software categorieën zijn vooraf gedefinieerd in de Asset Intelligence-catalogus. U kunt door de gebruiker gedefinieerde categorieën maken om geïnventariseerde software verder te definiëren. De validatie status voor alle vooraf gedefinieerde software categorieën is altijd **gevalideerd**. Aangepaste software categorie gegevens die zijn toegevoegd aan de Asset Intelligence-catalogus, worden door de **gebruiker gedefinieerd**. 

Zie [Asset Intelligence configureren](configuring-asset-intelligence.md)voor meer informatie over het beheren van software categorieën.  

> [!NOTE]  
> Vooraf gedefinieerde software categorie gegevens die zijn opgeslagen in de Asset Intelligence-catalogus, zijn alleen-lezen. U kunt deze niet wijzigen of verwijderen. Gebruikers met beheerdersrechten kunnen door de gebruiker gedefinieerde softwarecategorieën toevoegen, wijzigen of verwijderen.  


### <a name="software-families"></a><a name="BKMK_SoftwareFamilies"></a>Software families  

Asset Intelligence-software families worden gebruikt om geïnventariseerde software titels binnen software categorieën te definiëren. Veel software families zijn vooraf gedefinieerd in de Asset Intelligence-catalogus. U kunt door de gebruiker gedefinieerde categorieën maken om geïnventariseerde software verder te definiëren. De validatie status voor alle vooraf gedefinieerde software families wordt altijd **gevalideerd**. Informatie over aangepaste software familie die is toegevoegd aan de Asset Intelligence-catalogus, wordt door de **gebruiker gedefinieerd**. 

Zie [Asset Intelligence configureren](configuring-asset-intelligence.md)voor meer informatie over het beheren van software families.  

> [!NOTE]  
> Informatie over vooraf gedefinieerde software families is alleen-lezen en kan niet worden gewijzigd. Gebruikers met beheerdersrechten kunnen door de gebruiker gedefinieerde softwarefamilies toevoegen, wijzigen of verwijderen.  


### <a name="software-labels"></a><a name="BKMK_CustomLabels"></a> Softwarelabels  

Met de aangepaste software-labels Asset Intelligence kunt u filters maken voor het groeperen van software titels en deze weer geven in Asset Intelligence-rapporten. Gebruik software-labels voor het maken van door de gebruiker gedefinieerde groepen met software titels die een gemeen schappelijk kenmerk delen. U kunt bijvoorbeeld een software label maken met de naam shareware, deze koppelen aan geïnventariseerde shareware titels en een rapport uitvoeren om alle software titels met dat label weer te geven. Er zijn geen vooraf gedefinieerde labels. De validatiestatus voor softwarelabels is altijd **Door de gebruiker gedefinieerd**. 

Zie [Asset Intelligence configureren](configuring-asset-intelligence.md)voor meer informatie over het beheren van software-labels.  


### <a name="hardware-requirements"></a><a name="BKMK_HardwareRequirements"></a>Hardwarevereisten  

Gebruik de informatie over de hardwarevereisten om te controleren of computers voldoen aan de hardwarevereisten voor software titels voordat ze worden bedoeld voor software-implementaties. Hardware-vereisten voor software titels beheren in de werk ruimte **activa en naleving** in het knoop punt **hardwarevereisten** onder het knoop punt **Asset Intelligence** . 

Veel hardwarevereisten zijn vooraf gedefinieerd in de Asset Intelligence-catalogus. Nieuwe door de gebruiker gedefinieerde informatie over vereiste hardware maken om te voldoen aan aangepaste vereisten. De validatie status voor alle vooraf gedefinieerde hardwarevereisten wordt altijd **gevalideerd**. Informatie over door de gebruiker gedefinieerde hardwarevereisten die aan de Asset Intelligence-catalogus is toegevoegd, is door de **gebruiker gedefinieerd**. 

Zie [Asset Intelligence configureren](configuring-asset-intelligence.md)voor meer informatie over het beheren van hardwarevereisten.  

> [!NOTE]  
> De hardwarevereisten die worden weer gegeven in de Configuration Manager-console, worden opgehaald uit de Asset Intelligence-catalogus. Ze zijn niet gebaseerd op informatie over geïnventariseerde software titels van-clients. 
> 
> Informatie over hardwarevereisten wordt niet bijgewerkt als onderdeel van het synchronisatie proces met micro soft. 
> 
> U kunt door de gebruiker gedefinieerde hardwarevereisten maken voor geïnventariseerde software waaraan geen vereisten voor de hardwarevereisten zijn gekoppeld.  

Standaard wordt de volgende informatie weergegeven voor elke vermelde hardwarevereiste:  

- **Software titel**: de software titel van de vereiste hardware  

- **Minimale CPU (MHz)**: de minimale processor snelheid, in Mega Hertz (MHz), die wordt vereist door de software titel  

- **Mini maal RAM (KB)**: de minimale hoeveelheid RAM (in KB) die is vereist voor de software titel  

- **Minimale schijf ruimte (KB)**: de minimale vrije schijf ruimte in KB die vereist is voor de software titel  

- **Minimale schijf grootte (KB)**: de minimale grootte van de harde schijf in KB die vereist is voor de software titel  

- **Validatie status**: de validatie status voor de vereiste hardware  

Vooraf gedefinieerde hardwarevereisten die zijn opgeslagen in de Asset Intelligence-catalogus, zijn alleen-lezen en kunnen niet worden verwijderd. Gebruikers met beheerders rechten kunnen door de gebruiker gedefinieerde hardwarevereisten toevoegen, wijzigen of verwijderen voor software titels die niet in de Asset Intelligence-catalogus zijn opgeslagen.  



## <a name="inventoried-software-titles"></a><a name="BKMK_InventoriedSoftwareTitles"></a>Geïnventariseerde software titels  

Als u informatie over de geïnventariseerde software titel in de Configuration Manager-console wilt weer geven, gaat u naar de werk ruimte **activa en naleving** , vouwt u het knoop punt **Asset Intelligence** uit en selecteert u het knoop punt **geïnventariseerde software** . De hardware-inventaris agent verzamelt de geïnventariseerde software-informatie van Configuration Manager-clients op basis van de software titels die zijn opgeslagen in de Asset Intelligence-catalogus.  

> [!Note]  
> De hardware-inventaris agent verzamelt inventaris op basis van de Asset Intelligence-rapportage klassen voor hardware-inventarisatie die u inschakelt. Zie [Asset Intelligence configureren](configuring-asset-intelligence.md)voor meer informatie over het inschakelen van de rapportage klassen.  

Standaard wordt de volgende informatie weergegeven voor elke geïnventariseerde softwaretitel:  

- **Naam**: de naam van de geïnventariseerde software titel  

- **Leverancier**: de naam van de leverancier die de geïnventariseerde software titel heeft ontwikkeld  

- **Versie**: de product versie van de geïnventariseerde software titel  

- **Categorie**: de software categorie die momenteel is toegewezen aan de geïnventariseerde software titel  

- **Family**: de software familie die momenteel is toegewezen aan de geïnventariseerde software titel  

- **Label** [**1**, **2**en **3**]: de aangepaste labels die zijn gekoppeld aan de software titel. Aan geïnventariseerde softwaretitels kunnen maximaal drie aangepaste labels worden gekoppeld.  

- **Aantal**: het aantal Configuration Manager-clients dat de software titel heeft geïnventariseerd  

- **Status**: de validatie status voor de geïnventariseerde software titel  

> [!NOTE]  
> U kunt de categorisatie-informatie voor geïnventariseerde software alleen wijzigen op de site op het hoogste niveau in uw hiërarchie. Deze informatie omvat product naam, leverancier, software categorie en software familie. Wanneer u categorisatiegegevens voor vooraf gedefinieerde software wijzigt, wordt de validatiestatus voor de software gewijzigd van **Gevalideerd** in **Door de gebruiker gedefinieerd**.  



## <a name="asset-intelligence-synchronization-point"></a><a name="AssetIntelligenceSycnronizationPoint"></a>Asset Intelligence-synchronisatie punt  

Het Asset Intelligence-synchronisatie punt is een Configuration Manager site systeemrol. Het wordt gebruikt om verbinding te maken met de micro soft-Cloud op TCP-poort 443 om updates van dynamische catalogus gegevens te beheren. Installeer deze siterol alleen op de site op het hoogste niveau van de hiërarchie. Alle Asset Intelligence-catalogus aanpassingen configureren met behulp van een Configuration Manager-console die is verbonden met de site op het hoogste niveau. 

Wanneer u alle updates op de site op het hoogste niveau configureert, worden de catalogus gegevens gerepliceerd naar andere sites in de hiërarchie. Met de siterol kunt u catalogus synchronisatie op aanvraag met micro soft aanvragen of automatische catalogus synchronisatie plannen. Naast het downloaden van nieuwe catalogus gegevens, kunnen met het Asset Intelligence-synchronisatie punt informatie over aangepaste software titels voor categorisatie naar micro soft worden geüpload. Micro soft behandelt alle geüploade software titels als open bare informatie. Zorg ervoor dat uw aangepaste software titels geen vertrouwelijke of eigendoms informatie bevatten.  

Nadat u een niet-gecategoriseerde software titel hebt ingediend, wordt deze niet door micro soft gecontroleerd totdat er ten minste vier categorisatie aanvragen van klanten voor dezelfde software titel zijn. Micro soft-onderzoekers identificeren, categoriseren en maken de software titel categorisatie-informatie beschikbaar voor alle klanten die de online service gebruiken. Softwaretitels met de meeste aanvragen voor categorisatie krijgen de hoogste prioriteit. Aangepaste software-en line-of-business-toepassingen zijn waarschijnlijk niet in een categorie te ontvangen. Stuur deze software titels niet naar micro soft voor categorisatie.  

Een Asset Intelligence-synchronisatie punt is vereist om verbinding te maken met de micro soft-Cloud. Zie [Asset Intelligence configureren](configuring-asset-intelligence.md)voor meer informatie over het installeren van de rol.  



## <a name="asset-intelligence-home-page"></a><a name="BKMK_AssetIntelligenceHomePage"></a>Start pagina Asset Intelligence  

Het knoop punt **Asset Intelligence** in de werk ruimte **activa en naleving** is de start pagina voor Asset Intelligence in Configuration Manager. Op deze start pagina wordt een overzichts dashboard weer gegeven voor Asset Intelligence-catalogus informatie.  

> [!NOTE]  
> De start pagina van **Asset Intelligence** wordt niet automatisch bijgewerkt wanneer u deze weergeeft.  

De **Asset Intelligence** start pagina bevat de volgende secties:  

- **Catalogus synchronisatie**: informatie over of Asset Intelligence is ingeschakeld en de huidige status van het Asset Intelligence-synchronisatie punt.  

    > [!NOTE]  
    > Op de start pagina wordt deze sectie alleen weer gegeven wanneer u een Asset Intelligence-synchronisatie punt installeert.  

    De sectie bevat ook de volgende informatie:  

    - Synchronisatieplanning  

    - Als u een klant licentie verklaring hebt geïmporteerd   

    - De laatste status update  

    - De tijd voor de volgende geplande update  

    - Het aantal wijzigingen na de installatie van het Asset Intelligence-synchronisatie punt   

- **Status geïnventariseerde software**: de telling en het percentage van geïnventariseerde software, software categorieën en software families die door micro soft worden geïdentificeerd, geïdentificeerd door een beheerder, in afwachting van online identificatie of niet in behandeling. De informatie in tabelindeling bevat het aantal voor elke softwaretoepassing, terwijl in de grafiek het percentage voor elke softwaretoepassing wordt weergegeven.  



## <a name="asset-intelligence-reports"></a><a name="BKMK_AssetIntelligenceReports"></a>Asset Intelligence-rapporten  

De Asset Intelligence-rapporten bevinden zich in de Configuration Manager-console, in de werk ruimte **bewaking** , in de map **Asset Intelligence** onder het knoop punt **rapportage** . De rapporten bevatten informatie over de hardware, licentiebeheer en software. Zie [Introduction to Reporting](../../../servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie over rapporten in Configuration Manager.  

> [!NOTE]  
> De nauw keurigheid van het aantal geïnstalleerde software titels en de weer gegeven licentie gegevens in Asset Intelligence-rapporten kan afwijken van het werkelijke aantal geïnstalleerde software titels of licenties die in de omgeving worden gebruikt. Deze afwijking wordt veroorzaakt door de complexe afhankelijkheden en beperkingen bij het inventariseren van softwarelicentiegegevens voor softwaretitels die zijn geïnstalleerd in bedrijfsomgevingen. Gebruik geen Asset Intelligence-rapporten als de enige bron voor het bepalen van de naleving van gekochte software licenties.  


### <a name="hardware-reports"></a><a name="BKMK_HardwareReports"></a>Hardware-rapporten  

Asset Intelligence-hardware-rapporten bieden informatie over hardware-assets in de organisatie. Met hardware-inventarisatie gegevens, zoals snelheid, geheugen en rand apparatuur, kunnen Asset Intelligence-hardware-rapporten informatie over USB-apparaten, hardware die moet worden bijgewerkt en zelfs computers die niet gereed zijn voor een bepaalde software-upgrade presen teren.  

> [!NOTE]  
> Bepaalde gebruikers gegevens in Asset Intelligence-hardware-rapporten worden verzameld uit het Windows-beveiligings logboek. Voor een betere nauw keurigheid van het rapport kunt u dit logboek wissen wanneer u een computer opnieuw toewijst aan een nieuwe gebruiker.  


### <a name="license-management-reports"></a><a name="BKMK_LicenseManagementReports"></a>Rapporten voor licentie beheer  

Asset Intelligence-rapporten voor licentie beheer bevatten gegevens over licenties die worden gebruikt. In het rapport **licentie-grootboek** worden geïnstalleerde micro soft-toepassingen weer gegeven in een indeling congruent met een micro soft-licentie verklaring (MLS). Deze indeling biedt een handige methode voor het vergelijken van de aangeschafte licenties met gebruikte licenties. Andere rapporten voor licentie beheer bieden informatie over computers die fungeren als servers waarop de Key Management service (KMS) voor Windows-activerings statistieken worden uitgevoerd.  

> [!IMPORTANT]  
> Diverse Asset Intelligence-licentie beheer rapporten bevatten informatie over de functie van KMS, een methode voor het beheren van volume licenties. Als u nog geen KMS-server hebt geïmplementeerd, retour neren sommige rapporten mogelijk geen gegevens.  


### <a name="software-reports"></a><a name="BKMK_SoftwareReports"></a>Software rapporten  

Asset Intelligence-software rapporten bevatten informatie over software families, categorieën en specifieke software titels die zijn geïnstalleerd op computers in de organisatie. Het software rapport bevat informatie zoals browserhelperobjecten en software die automatisch wordt gestart. Deze rapporten kunnen worden gebruikt om adware, spyware en andere schadelijke software te identificeren. U kunt ze ook gebruiken om software-redundantie te identificeren om software-aanschaf en-ondersteuning te stroom lijnen.  


### <a name="software-identification-tag-reports"></a><a name="BKMK_SoftwareIdTagReports"></a>Software-id-label rapporten  

Asset Intelligence software Identification tag-rapporten bevatten informatie over software die een software-ID-tag bevat die voldoet aan ISO/IEC 19770-2. De software-ID-Tags bieden gezaghebbende informatie die wordt gebruikt voor het identificeren van geïnstalleerde software. Wanneer u de **SMS_SoftwareTag** rapportage klasse voor hardware-inventarisatie inschakelt, Configuration Manager verzamelde informatie over de software met software-identificatie tags. 

De volgende rapporten bevatten informatie over de software:  

- **Software 14 bis-zoeken naar software Identification tag enabled software**: het aantal geïnstalleerde software waarvoor een software-ID-tag is ingeschakeld  

- **Software 14%-computers waarop bepaalde software met software-identificatie tags is geïnstalleerd**: alle computers waarop software is geïnstalleerd met een specifieke software-ID-tag ingeschakeld  

- **Software 14 quater-geïnstalleerde software met software-identificatie label ingeschakeld op een specifieke computer**: alle geïnstalleerde software met een specifieke software-ID-tag ingeschakeld op een specifieke computer  


### <a name="reporting-limitations"></a><a name="BKMK_ReportingLImitations"></a>Rapportage beperkingen  

Asset Intelligence-rapporten kunnen grote hoeveel heden informatie bieden over geïnstalleerde software titels en de software licenties die worden gebruikt, hebben verkregen. Gebruik deze informatie niet als de enige bron voor het bepalen van de naleving van de aanschaf van de software.  

#### <a name="example-dependencies"></a><a name="BKMK_ExampleDependencies"></a> Voorbeelden van afhankelijkheden  
De nauw keurigheid van het aantal dat wordt weer gegeven in de Asset Intelligence-rapporten voor geïnstalleerde software titels en licentie gegevens kan afwijken van de werkelijke hoeveel heden die momenteel worden gebruikt. Deze afwijking wordt veroorzaakt door de complexe afhankelijkheden bij het inventariseren van softwarelicentiegegevens voor softwaretitels die worden gebruikt in bedrijfsomgevingen. In de volgende voor beelden ziet u de afhankelijkheden die zijn betrokken bij het inventariseren van geïnstalleerde software in het bedrijf met Asset Intelligence die van invloed kan zijn op de nauw keurigheid van Asset Intelligence-rapporten:  

- **Afhankelijkheden voor hardware-inventaris van client**: Asset Intelligence geïnstalleerde software rapporten zijn gebaseerd op gegevens die worden verzameld van Configuration Manager clients door de hardware-inventaris uit te breiden om Asset Intelligence-rapportage mogelijk te maken. Vanwege deze afhankelijkheid van hardware-inventaris rapportage, geven Asset Intelligence-rapporten alleen gegevens weer van clients die hardware-inventarisatie processen hebben voltooid met de vereiste Asset Intelligence WMI-rapportage klassen ingeschakeld. Omdat Configuration Manager-clients Hardware-inventarisatie processen uitvoeren volgens een schema dat is gedefinieerd door de gebruiker met beheerders rechten, kan er een vertraging optreden in de gegevens rapportage die van invloed is op de nauw keurigheid van Asset Intelligence-rapporten. 

    Een geïnventariseerde gelicentieerde softwaretitel kan bijvoorbeeld zijn verwijderd nadat op de client een geslaagde hardware-inventarisatiecyclus is uitgevoerd. Asset Intelligence-rapporten geven de software titel weer zoals deze is geïnstalleerd tot de volgende geplande cyclus voor hardware-inventaris rapportage door de client wordt uitgevoerd.  

- **Afhankelijkheden van software pakketten**: Asset Intelligence-rapporten zijn gebaseerd op geïnstalleerde software titel gegevens die worden verzameld met behulp van standaard Configuration Manager Hardware-inventarisatie processen van de client. Bepaalde software titel gegevens worden mogelijk niet correct verzameld. Voor beelden die kunnen leiden tot onnauwkeurige Asset Intelligence-rapportage:  

    - Software-installaties die niet voldoen aan standaard installatie processen  

    - Software-installaties die zijn gewijzigd vóór de installatie   

#### <a name="legal-limitations"></a><a name="BKMK_LegalLimitations"></a> Juridische beperkingen  
De informatie die wordt weer gegeven in Asset Intelligence-rapporten is onderhevig aan veel beperkingen. De gegevens die hierin worden weer gegeven, vertegenwoordigen geen juridisch, boekhoud kundig of ander professioneel advies. De informatie die wordt verstrekt door Asset Intelligence-rapporten is alleen ter informatie. Gebruik deze niet als de enige bron van informatie voor het bepalen van de naleving van het gebruik van software licenties.  

De volgende beperkingen zijn voor beelden van het gebruik van Asset Intelligence die van invloed kunnen zijn op de nauw keurigheid van de rapporten:  

- **Beperkingen voor gebruiks aantallen van micro soft-licenties**:  

    - Het aantal verworven micro soft-software licenties is gebaseerd op informatie die door de beheerder wordt verstrekt. Bekijk deze nauw keurig om er zeker van te zijn dat het juiste aantal software licenties wordt verstrekt.  

    - De gerapporteerde hoeveelheid micro soft-software licenties bevat alleen informatie over micro soft-software licenties die zijn verkregen via volume licentie Programma's. Er wordt geen informatie weer gegeven voor software licenties die zijn verkregen via retail-, OEM-of andere software licentie verkoop kanalen.  

    - Softwarelicenties die de afgelopen 45 dagen zijn aangeschaft, worden mogelijk niet opgenomen in het aantal gerapporteerde Microsoft-softwarelicenties vanwege rapportagevereisten en -planningen van softwareverkopers.  

    - Overdrachten van softwarelicenties vanwege bedrijfsfusies of -overnames worden mogelijk niet weerspiegeld in gerapporteerde aantallen van Microsoft-softwarelicenties.  

    - Niet-standaard voorwaarden en-bepalingen in een micro soft Volume Licensing-overeenkomst zijn mogelijk van invloed op het aantal gemelde software licenties. Ze hebben mogelijk extra beoordeling nodig door een micro soft-vertegenwoordiger.  

- **Beperkingen voor het aantal geïnstalleerde software titels**: Configuration Manager-clients moeten de rapportage cycli voor hardware-inventarisatie met succes volt ooien voor de Asset Intelligence-rapporten om nauw keurig het aantal geïnstalleerde software titels te rapporteren. Er kan een vertraging optreden tussen het installeren of verwijderen van een gelicentieerde software titel na een geslaagde rapportage cyclus voor hardware-inventarisatie. Deze actie wordt mogelijk niet weer gegeven in Asset Intelligence-rapporten die worden uitgevoerd voordat de client de volgende geplande hardware-inventaris meldt.  

- **Beperkingen voor licentie afstemming**: de aansluiting van het aantal geïnstalleerde software titels op het aantal aangeschafte software licenties wordt berekend met behulp van een vergelijking van het aantal licenties dat is opgegeven door de beheerder en het aantal geïnstalleerde software titels dat is verzameld van Configuration Manager hardware-inventarisaties van de client op basis van de planning die is ingesteld door de beheerder. Deze vergelijking vertegenwoordigt geen definitieve micro soft-conclusie van de licentie posities. De werkelijke licentiepositie is afhankelijk van de specifieke softwaretitellicentie en verleende gebruiksrechten door de licentievoorwaarden.  



## <a name="asset-intelligence-validation-states"></a><a name="BKMK_ValidationStates"></a>Statussen van Asset Intelligence-validatie  

Statussen van Asset Intelligence-validatie vertegenwoordigen de bron-en huidige validatie status van Asset Intelligence-catalogus gegevens. De volgende tabel bevat mogelijke Asset Intelligence-validatie statussen en beheerder acties die deze kunnen veroorzaken.  

| Status | Definitie | Beheerdersactie | Opmerking |  
|---------------|--------------------|------------------------------|-----------------|  
|**Gevalideerd**|Micro soft-onderzoekers hebben het catalogus item gedefinieerd|Geen|Beste status|  
|**Door de gebruiker gedefinieerd**|Micro soft-onderzoekers hebben het catalogus item niet gedefinieerd|De gegevens van de lokale catalogus aanpassen|Deze status wordt weer gegeven in Asset Intelligence-rapporten|  
|**In behandeling**|Micro soft-onderzoekers hebben het catalogus item niet gedefinieerd, maar u hebt het item voor categorisatie naar micro soft verzonden|Geen verdere actie na het aanvragen van categorisatie|Het catalogus item behoudt deze status totdat het onderzoeksteam van micro soft het item heeft gecategoriseerd en u uw Asset Intelligence-catalogus synchroniseert.|  
|**Bij te werken**|Een door de gebruiker gedefinieerd catalogus item is door micro soft anders gecategoriseerd tijdens de synchronisatie van de catalogus.|Gebruik de actie **conflict oplossen** om te bepalen of u de nieuwe categorisatie gegevens of de vorige door de gebruiker gedefinieerde waarde wilt gebruiken. Zie [bewerkingen voor Asset Intelligence](operations-for-asset-intelligence.md)voor meer informatie over het oplossen van conflicten.|Nadat u een categorisatie conflict hebt opgelost, wordt het item niet gevalideerd als conflicterend tenzij latere categorisatie-updates nieuwe informatie over het item introduceren.|  
|**Niet-gecategoriseerd**|Catalogus item is niet gedefinieerd door micro soft-onderzoekers, het item is niet voor categorisatie naar micro soft verzonden en de beheerder heeft geen door de gebruiker gedefinieerde categorisatie waarde toegewezen.|Vraag categorisatie aan of pas uw lokale catalogus gegevens aan. Zie [bewerkingen voor Asset Intelligence](operations-for-asset-intelligence.md)voor meer informatie.|Geen|  

> [!NOTE]  
> Catalogus items die u voor categorisatie naar micro soft verzendt, hebben de validatie status **in behandeling** op een centrale beheer site, maar worden nog steeds weer gegeven met de validatie status niet- **gecategoriseerd** op onderliggende primaire sites.  

Zie [voorbeeld validatie status overgangen voor Asset Intelligence](example-validation-state-transitions-for-asset-intelligence.md)voor voor beelden van wanneer een validatie status van de ene status naar de andere kan worden overgezet.  
