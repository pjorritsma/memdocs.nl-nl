---
title: Inleiding tot software-updates
titleSuffix: Configuration Manager
description: Meer informatie over de basis principes van software-updates in Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 10/30/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9778b13-c8a3-40eb-8655-34ac8ce9cdaa
ms.openlocfilehash: c857997bdbeed51286e874dcbecf00b414dfe6a0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717641"
---
# <a name="introduction-to-software-updates-in-configuration-manager"></a>Inleiding tot software-updates in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Software-updates in Configuration Manager biedt een set hulpprogram ma's en bronnen waarmee u de complexe taak voor het bijhouden en Toep assen van software-updates op client computers in de onderneming kunt beheren. Een effectief beheerproces van software-update is nodig om operationele efficiëntie te behouden, om beveiligingsproblemen te overwinnen en om de stabiliteit van de netwerkinfrastructuur te behouden. Wegens de veranderende aard van technologie en het permanent opduiken van nieuwe veiligheidsbedreigingen, vergt effectief beheer van software-updates consistente en continue aandacht.  

Zie voor een voorbeeld scenario waarin wordt getoond hoe u software-updates in uw omgeving kunt implementeren, [voorbeeld scenario voor het implementeren van beveiligings software-updates](../deploy-use/example-scenario-deploy-monitor-monthly-security-updates.md).  

##  <a name="software-updates-synchronization"></a><a name="BKMK_Synchronization"></a> Synchronisatie van software-updates  
 Synchronisatie van software-updates in Configuration Manager maakt verbinding met Microsoft Update om meta gegevens van software-updates op te halen. De site op het hoogste niveau (centrale beheer site of zelfstandige primaire site) synchroniseert met Microsoft Update volgens een planning of wanneer u de synchronisatie hand matig start vanuit de Configuration Manager-console. Wanneer de synchronisatie van software-updates op de site op het hoogste niveau Configuration Manager voltooid, wordt de synchronisatie van software-updates gestart op onderliggende sites, indien aanwezig. Wanneer synchronisatie volledig is op de primaire site of secundaire site, wordt een beleid voor de hele site gemaakt, dat de clientcomputers de locatie van software-updatepunten levert.  

> [!NOTE]  
>  Software-updates zijn in de clientinstellingen standaard ingeschakeld. Indien u evenwel de clientinstelling **Software-updates inschakelen op clients** instelt op **Nee** om software-updates uit te schakelen op een verzameling of in de standaardinstellingen, worden de locaties van software-updatepunten niet gezonden naar gekoppelde clients. Zie [client instellingen voor software-updates](../../core/clients/deploy/about-client-settings.md#software-updates)voor meer informatie.  

 Nadat de client het beleid ontvangt, start de client een scan voor naleving van software-updates en schrijft de informatie naar Windows Management Instrumentation (WMI). De informatie over naleving wordt dan gezonden naar het beheerpunt dat dan de informatie naar de siteserver zendt. Zie de sectie [Software updates compliance assessment](#BKMK_SUMCompliance) van dit onderwerp voor meer informatie over nalevingsbeoordeling.  

 U kunt meerdere software-updatepunten installeren in een primaire site. Het eerste software-updatepunt dat u installeert is geconfigureerd als de synchronisatiebron. Hiermee synchroniseert u van Microsoft Update of een WSUS-server die niet in uw Configuration Manager hiërarchie voor komt. De andere software-updatepunten op de site gebruiken het eerste software-updatepunt als de synchronisatiebron.  

> [!NOTE]  
>  Wanneer het proces van synchronisatie van software-updates volledig is op de site van het hoogste niveau, worden de metagegevens van software-updates gerepliceerd naar onderliggende sites door gebruik te maken van databasereplicatie. Wanneer u een Configuration Manager-console verbindt met de onderliggende site, Configuration Manager de meta gegevens van software-updates weer gegeven. Voordat u echter een software-update punt installeert en configureert op de site, zullen clients niet scannen op naleving van software-updates, zullen clients geen compatibiliteits informatie rapporteren aan Configuration Manager en kunt u geen software-updates implementeren.  

### <a name="synchronization-on-the-top-level-site"></a>Synchronisatie in de site op het hoogste niveau  
 Het proces van synchronisatie van software-updates op de site van het hoogste niveau, onttrekt de metagegevens voor software-updates van Microsoft Update, die voldoen aan de criteria die u opgeeft in de eigenschappen van onderdeel software-updatepunt U kunt de criteria alleen op de site het hoogste niveau configureren.  

> [!NOTE]  
>  U kunt een bestaande WSUS-server die zich niet in de Configuration Manager-hiërarchie bevindt, in plaats van micro soft-updates opgeven als de synchronisatie bron.  

 De volgende lijst beschrijft de basisstappen voor het synchronisatieproces op de site van het hoogste niveau:  

1.  Synchronisatie van software-updates wordt gestart.  

2.  WSUS Synchronization Manager zendt een verzoek naar WSUS dat uitgevoerd wordt op het software-updatepunt, om synchronisatie te starten met Microsoft Update.  

3.  De metagegevens van software-updates worden gesynchroniseerd door Microsoft Update, en wijzigingen worden toegevoegd of geüpdatet in de WSUS-database.  

4.  Wanneer WSUS is gesynchroniseerd, synchroniseert WSUS Synchronization Manager de meta gegevens van software-updates van de WSUS-Data Base naar de Configuration Manager-Data Base en worden eventuele wijzigingen na de laatste synchronisatie in de site database ingevoegd of bijgewerkt. De metagegevens van de software-updates worden opgeslagen in de site-database als een configuratie-item.  

5.  De configuratie-items van software-updates worden gezonden naar onderliggende sites door gebruik te maken van databasereplicatie.  

6.  Wanneer synchronisatie is voltooid, maakt de WSUS Synchronization Manager een statusbericht 6702.  

7.  WSUS Synchronization Manager zendt een synchronisatieverzoek naar alle onderliggende sites.  

8.  WSUS Synchronization Manager zendt één verzoek per keer naar WSUS die uitgevoerd wordt op andere software-updatepunten op de site. De WSUS-servers op de andere software-updatepunten zijn geconfigureerd om replica's te zijn van WSUS, die uitgevoerd wordt op het standaard-updatepunt op de site.  

### <a name="synchronization-on-child-primary-and-secondary-sites"></a>Synchronisatie in de onderliggende primaire en secundaire sites  
 Wanneer het proces van synchronisatie van software-updates volledig is op de site van het hoogste niveau, worden de configuratie-items van de software-updates gerepliceerd naar onderliggende sites door gebruik te maken van databasereplicatie. Op het einde van het proces zendt de site op het hoogste niveau een synchronisatieverzoek naar de onderliggende site en de onderliggende site start de WSUS-synchronisatie. De volgende lijst beschrijft de basisstappen voor het synchronisatieproces op een onderliggende primaire site of op een secundaire site:  

1.  WSUS Synchronization Manager zendt een synchronisatieverzoek vanaf de site van het hoogste niveau.  

2.  Synchronisatie van software-updates wordt gestart.  

3.  WSUS Synchronization Manager zendt een verzoek naar WSUS die uitgevoerd wordt op het software-updatepunt, om synchronisatie te starten.  

4.  WSUS die uitgevoerd wordt op het software-updatepunt op de onderliggende site synchroniseert metagegevens van software-updates vanaf WSUS die uitgevoerd wordt op het software-updatepunt op de bovenliggende site.  

5.  Wanneer synchronisatie is voltooid, maakt de WSUS Synchronization Manager een statusbericht 6702.  

6.  Vanaf een primaire site zendt WSUS Synchronization Manager een synchronisatieverzoek naar alle onderliggende, secundaire sites. De secundaire site start de synchronisatie van software-updates met de bovenliggende primaire site. De secundaire site is geconfigureerd als een replica van WSUS die uitgevoerd wordt op de bovenliggende site.  

7.  WSUS Synchronization Manager zendt één verzoek per keer naar WSUS die uitgevoerd wordt op andere software-updatepunten op de site. De WSUS-servers op de andere software-updatepunten zijn geconfigureerd om replica's te zijn van WSUS, die uitgevoerd wordt op het standaard-updatepunt op de site.  

##  <a name="software-updates-compliance-assessment"></a><a name="BKMK_SUMCompliance"></a> Software updates compliance assessment  
 Voordat u software-updates implementeert op client computers in Configuration Manager, start u een scan voor compatibiliteit van software-updates op client computers. Voor elke software-update wordt een statusbericht gemaakt dat de nalevingsstatus bevat voor de update. De statusberichten worden in bulk gezonden naar het beheerpunt en dan naar de siteserver, waar de nalevingstatus ingevoegd wordt in de sitedatabase. De nalevings status voor software-updates wordt weer gegeven in de Configuration Manager-console. U kunt software-updates implementeren en installeren op computers die de updates nodig hebben. De volgende secties geven informatie over de nalevingsstatussen en beschrijven het proces van scannen voor naleving van software-updates  

### <a name="software-updates-compliance-states"></a>Nalevingsstatussen voor software-updates  
 Hieronder vindt u een overzicht en een beschrijving van elke nalevings status die wordt weer gegeven in de Configuration Manager-console voor software-updates.  

-   **Vereist**  

     Specificeert dat de software-update toepasselijk is en nodig op de clientcomputer Eén van de volgende condities kan waar zijn wanneer de software-updatestatus **Vereist**is:  

    -   De software-update is niet geïmplementeerd op de clientcomputer.  

    -   De software-update is geïnstalleerd op de clientcomputer. Evenwel is het meest recente statusbericht nog niet ingevoegd in de database op de siteserver. De clientcomputer scant opnieuw voor de update nadat de installatie voltooid is. Er kan een vertraging zijn tot twee minuten vóór de client de geüpdate toestand zendt naar het beheerpunt dat dan de geüpdate toestand doorstuurt naar de siteserver.  

    -   De software-update is geïnstalleerd op de clientcomputer. De software-update-installatie vereist evenwel een opnieuw opstarten van de computer vóór de update voltooid is.  

    -   De software-update werd geïmplementeerd naar de clientcomputer maar werd nog niet geïnstalleerd.  

-   **Niet vereist**  

     Geeft op dat de software-update niet toepasselijk is op de clientcomputer. De software-update is daarom niet vereist.  

-   **Geïnstalleerd**  

     Geeft op dat de software-update toepasselijk is op de clientcomputer en dat de clientcomputer de software-update reeds geïnstalleerd heeft.  

-   **Onbekend**  

     Geeft op dat de siteserver geen statusbericht heeft ontvangen van de clientcomputer, typisch wegens één van de volgende redenen:  

    -   De clientcomputer heeft niet met succes gescand op naleving van software-updates.  

    -   De scan is voltooid op de clientcomputer. Het statusbericht werd nog niet verwerkt op de siteserver, eventueel omwille van een achterstand van de statusberichten.  

    -   De scan werd voltooid op de clientcomputer, maar het statusbericht werd nog niet ontvangen van de onderliggende site.  

    -   De scan werd voltooid op de clientcomputer, maar het statusberichtenbestand werd op één of andere manier beschadigd en kon niet verwerkt worden.  

### <a name="scan-for-software-updates-compliance-process"></a>Het scannen op de naleving voor software-updates  
 Wanneer het software-update punt is geïnstalleerd en gesynchroniseerd, wordt een computer beleid voor de hele site gemaakt waarmee de client computers worden geïnformeerd dat Configuration Manager software-updates zijn ingeschakeld voor de site. Wanneer een client een computerbeleid ontvangt, wordt een scan gepland, die willekeurig binnen de komende twee uren kan beginnen, om de naleving te beoordelen. Wanneer de scan is gestart, wist een clientagent-proces voor software updates de geschiedenis van de scan, verzendt een verzoek om de WSUS-server te vinden die moet gebruikt worden voor de scan, en werkt het beleid van de lokale groep bij met de WSUS-serverlocatie.  

> [!NOTE]  
>  Internetclients moeten zich verbinden met de WSUS-server door gebruik te maken van SSL.  

 Een scanaanvraag wordt doorgegeven aan de Windows Update Agent (WUA). De WUA verbindt vervolgens met de WSUS-serverlocatie die wordt vermeld in het lokale beleid, haalt de metagegevens van de software-updates op die zijn gesynchroniseerd op de WSUS-server en scant de clientcomputer voor de updates. Een clientagentproces voor software-updates detecteert dat de compatibiliteitsscan is voltooid en maakt de statusberichten voor elke software-update waarvan de compatibiliteitsstatus is gewijzigd na de laatste scan. De statusberichten worden elke 15 minuten in bulk naar het beheerpunt verzonden. Het beheerpunt stuurt vervolgens de statusberichten naar de siteserver door; daar worden de statusberichten toegevoegd aan de siteserverdatabase.  

 Na de initiële scan voor compatibiliteit van software-updates, wordt de scan gestart volgens het geconfigureerde schema voor scannen. Als de client echter gescand heeft naar de compatibiliteit van software-updates binnen de door Time to Live (TTL) aangeduide tijdspanne, dan gebruikt deze de metagegevens van de software-updates die lokaal worden opgeslagen. Als de laatste scan zich buiten de TTL bevindt, moet de client verbinding maken met WSUS dat wordt uitgevoerd op het software-updatepunt en de metagegevens bijwerken van de software-updates die zijn opgeslagen op de clients.  

 Met inbegrip van het scanschema kan de scan voor compatibiliteit van de software-updates op de volgende manieren starten:  

-   **Scanschema voor software updates**: de scan voor compatibiliteit van software-updates begint bij het geconfigureerde scanschema dat wordt geconfigureerd in de instellingen van de clientagent voor software-updates. Zie [client instellingen voor software-updates](../../core/clients/deploy/about-client-settings.md#software-updates)voor meer informatie over het configureren van de client instellingen voor software-updates.  

-   **Actie voor Eigenschappen van Configuration Manager**: de gebruiker kan de actie **Scancyclus voor software-updates** of **Evaluatiecyclus voor de implementatie van software-updates** starten op het tabblad **Actie** in het dialoogvenster **Eigenschappen van Configuration Manager** op de clientcomputer.  

-   **Schema voor het opnieuw evalueren van implementaties**: de evaluatie van implementaties en de scan voor de compatibiliteit van software-updates begint bij het geconfigureerde schema voor het opnieuw evalueren van implementaties dat wordt geconfigureerd in de instellingen van de clientagent voor software-updates. Zie [client instellingen voor software-updates](../../core/clients/deploy/about-client-settings.md#software-updates)voor meer informatie over de client instellingen voor software-updates.  

-   **Voorafgaand aan het downloaden van de updatebestanden**: de clientagent voor software-updates downloadt de software-updates naar het lokale cachegeheugen van de client wanneer een clientcomputer een toewijzingsbeleid ontvangt voor een nieuwe vereiste implementatie. De clientagent start, vóór het downloaden van de software-updatebestanden, een scan om te verifiëren dat de software-update nog steeds vereist is.  

-   **Voorafgaand aan de installatie van software-updates**: de clientagent voor software-updates start, net vóór de installatie van de software-updates, een scan om te controleren of de software-updates nog steeds vereist zijn.  

-   **Na de installatie van software-updates**: gelijk na het voltooien van de installatie van een software-update, wordt door de clientagent voor software-updates een scan gestart om te controleren of de software-updates niet meer vereist zijn en wordt er een nieuw statusbericht gemaakt waarin wordt vermeld dat de software-update is geïnstalleerd. Als het na het voltooien van de installatie nodig is om opnieuw op te starten, geeft het statusbericht aan dat de clientcomputer wacht om opnieuw te worden opgestart.  

-   **Nadat het systeem opnieuw is opgestart**: als een clientcomputer wacht op het opnieuw opstarten van het systeem om de installatie van de software-update te voltooien, wordt door de clientagent voor software-updates een scan gestart na het opnieuw opstarten om te controleren of de software-update niet meer vereist is en wordt er een statusbericht gemaakt waarin wordt vermeld dat de software-update is geïnstalleerd.  

#### <a name="time-to-live-value"></a>De waarde Time to Live  
 De metagegevens van software-updates die zijn vereist voor de scan naar compatibiliteit van software-updates, worden opgeslagen op de lokale clientcomputer en zijn standaard tot 24 uur geldig. Deze waarde wordt aangeduid als de Time to Live (TTL).  

#### <a name="scan-for-software-updates-compliance-types"></a>Typen scans voor software-updatenaleving  
 De client scant naar de compatibiliteit van software-updates via een online of offline scan en een geforceerde of niet-geforceerde scan, afhankelijk van de manier waarop de scan voor software-updatecompatibiliteit wordt gestart. Hieronder wordt beschreven welke methoden voor het starten van de scan online of offline zijn en of de scan geforceerd of niet-geforceerd wordt afgedwongen.  

-   **Scan schema voor software-updates** (niet-geforceerde online scan)  

     Volgens het geconfigureerde scanschema verbindt de client met WSUS dat wordt uitgevoerd op het software-updatepunt om de metagegevens van de software-updates op te halen, alleen wanneer de laatste scan buiten de TTL werd uitgevoerd.  

-   **Evaluatie cyclus** voor de **Scan cyclus van software-updates** of de implementatie van software-updates (geforceerde online scan)  

     De clientcomputer maakt steeds verbinding met WSUS dat wordt uitgevoerd op het software-updatepunt voor het ophalen van de metagegevens van software-updates voordat de clientcomputer scant naar de compatibiliteit van software-updates. Nadat de scan is voltooid, wordt de TTL-teller opnieuw ingesteld. Als de TTL bijvoorbeeld 24 uur is, wordt de TTL opnieuw ingesteld op 24 uur nadat een gebruiker een scan start van de compatibiliteit van software-updates.  

-   **Planning** voor een nieuwe evaluatie van de implementatie (niet-geforceerde online scan)  

     Volgens het geconfigureerde implementatieschema voor nieuwe evaluaties verbindt de client met WSUS dat wordt uitgevoerd op het software-updatepunt om de metagegevens van de software-updates op te halen, alleen wanneer de laatste scan buiten de TTL werd uitgevoerd.  

-   **Vóór het downloaden van update bestanden** (niet-geforceerde online scan)  

     Voordat de client updatebestanden in de vereiste implementaties kan downloaden, verbindt de client met WSUS dat wordt uitgevoerd op het software-updatepunt om de metagegevens van de software-updates op te halen, alleen wanneer de laatste scan buiten de TTL werd uitgevoerd.  

-   **Vóór de installatie** van de software-update (niet-geforceerde online scan)  

     Voordat de client software-update installeert in de vereiste implementaties, verbindt de client met WSUS dat wordt uitgevoerd op het software-updatepunt om de metagegevens van de software-updates op te halen, alleen wanneer de laatste scan buiten de TTL werd uitgevoerd.  

-   **Na de installatie** van de software-update (geforceerde offline scan)  

     Na het installeren van een software-update, start de clientagent van software-updates een scan door gebruik te maken van de lokale metagegevens. De client maakt nooit verbinding met WSUS dat wordt uitgevoerd op het software-updatepunt om de metagegevens van software-updates op te halen.  

-   **Na opnieuw opstarten** van het systeem (geforceerde offline scan)  

     Na het installeren van een software-update en het opnieuw opstarten van de computer, start de clientagent van software-updates een scan door gebruik te maken van de lokale metagegevens. De client maakt nooit verbinding met WSUS dat wordt uitgevoerd op het software-updatepunt om de metagegevens van software-updates op te halen.  

##  <a name="software-update-deployment-packages"></a><a name="BKMK_DeploymentPackages"></a>Software-update-implementatie pakketten  
 Een implementatiepakket van een software-updatepunt is de drager die wordt gebruikt om software-updates naar een gedeelde netwerkmap te downloaden, en om de bronbestanden van de software-update te kopiëren naar de inhoudsbibliotheek op siteservers en op distributiepunten die in de implementatie worden gedefinieerd. Door de wizard Updates downloaden te gebruiken, kunt u software-updates downloaden en deze toevoegen aan implementatiepakketten voordat u ze implementeert. Met deze wizard kunt u software-updates inrichten op distributiepunten en verifiëren dat dit onderdeel van het implementatieproces succesvol is voordat u de software-updates naar clients implementeert.  

 De implementatie gebruikt automatisch het implementatiepakket dat de software-updates bevat als u gedownloade software-updates implementeert door gebruik te maken van de wizard Software-updates implementeren. Wanneer er software-updates worden geïmplementeerd die nog niet zijn gedownload, dient u een nieuw of bestaand implementatiepakket op te geven in de wizard Software-updates implementeren. De software-updates worden gedownload wanneer de wizard is voltooid.  

> [!IMPORTANT]  
>  U moet de gedeelde netwerkmap handmatig maken voor de bronbestanden van het installatiepakket voordat u het opgeeft in de wizard. Elk implementatiepakket moet een andere gedeelde netwerkmap gebruiken.  

> [!IMPORTANT]  
>  Het computeraccount van de SMS-provider en de gebruiker met beheerdersrechten die de software-updates effectief downloadt, hebben beide **Schrijf** machtigingen nodig voor de pakketbron. Beperk de toegang tot de pakketbron om het risico te beperken dat kwaadwillende personen knoeien met de bronbestanden van software-updates in de pakketbron.  

 Wanneer er een nieuw implementatiepakket wordt gemaakt, wordt de inhoudsversie op 1 ingesteld voordat er software-updates worden gedownload. Wanneer de software-updatebestanden worden gedownload met het pakket, wordt de inhoudsversie verhoogd naar 2. Daarom beginnen alle nieuwe implementatiepakketten met de inhoudsversie 2. Telkens wanneer de inhoud in een implementatiepakket wordt gewijzigd, wordt de inhoudsversie met 1 verhoogd. Zie [basis concepten voor inhouds beheer](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)voor meer informatie.  

 Clients installeren software-updates in een implementatie door gebruik te maken van een distributiepunt waarvan de software-updates beschikbaar zijn, onafhankelijk van het implementatiepakket. Zelfs als een implementatiepakket wordt verwijderd voor een actieve implementatie, kunnen clients nog steeds de software-updates installeren in de implementatie, zolang dat elke update naar minstens één ander implementatiepakket is gedownload en beschikbaar is op een distributiepunt dat kan worden bereikt vanaf de client. Wanneer het laatste implementatiepakket dat een software-update bevat, wordt verwijderd, kunnen clientcomputers de software-update niet ophalen totdat de update opnieuw wordt gedownload naar een implementatiepakket. Software-updates worden weer gegeven met een rode pijl in de Configuration Manager-console wanneer de update bestanden zich niet in implementatie pakketten bevinden. Implementaties worden weergegeven met een dubbele rode pijl als ze updates in deze toestand bevatten.  

##  <a name="software-update-deployment-workflows"></a><a name="BKMK_DeploymentWorkflows"></a> Werkstromen voor de implementatie van software-updates  
 Er zijn twee hoofdscenario's voor het implementeren van software-updates in uw omgeving: handmatige implementatie en automatische implementatie. Doorgaans kunt u software-updates handmatig implementeren om een basislijn voor clientcomputers te maken. Vervolgens beheert u software-updates op clients via automatische implementatie. De volgende secties bevatten een samenvatting van de werkstroom voor handmatige en automatische implementatie voor software-updates.  

###  <a name="manual-deployment-of-software-updates"></a><a name="BKMK_ManualDeployment"></a> Handmatige implementatie van software-updates  
 Hand matige implementatie van software-updates is het proces van het selecteren van software-updates in de Configuration Manager-console en het hand matig starten van het implementatie proces. Doorgaans gebruikt u deze methode van implementatie om de clientcomputers up-to-date te krijgen met de vereiste software-updates voordat u automatische implementatieregels kunt maken die de lopende maandelijkse implementaties van software-updates beheren, en om buiten-bandvereisten van software-updates te implementeren. De volgende lijst geeft de algemene werkstroom voor handmatige implementatie van software-updates:  

1.  Filter voor software-updates die gebruikmaken van specifieke vereisten. U kunt bijvoorbeeld criteria opgeven die alle beveiligingsupdates of kritieke software-updates ophalen die op meer dan 50 clientcomputers zijn vereist.  

2.  Maak een software-updategroep die de software-updates bevat.  

3.  Downloadt de inhoud voor software-updates in de software-updategroep.  

4.  De software-updategroep handmatig implementeren.  

###  <a name="automatic-deployment-of-software-updates"></a><a name="BKMK_AutomaticDeployment"></a> Automatische implementatie van software-updates  
 De automatische implementatie van software-updates wordt geconfigureerd met een regel voor automatische implementatie (ADR). Doorgaans gebruikt u deze methode voor uw maandelijkse software-updates (ook wel bekend als 'patchdinsdag') en voor het beheren van definitie-updates. Wanneer de regel wordt uitgevoerd, worden software-updates verwijderd van de software-updategroep (als u een bestaande groep gebruikt). De software-updates die voldoen aan een bepaald criterium (bijvoorbeeld alle softwarebeveiligingsupdates van de afgelopen week) worden toegevoegd aan een software-updategroep. De inhoudsbestanden voor de software-updates worden gedownload en gekopieerd naar de distributiepunten en de software-updates worden geïmplementeerd op clientcomputers in de doelverzameling. De volgende lijst geeft de algemene werkstroom voor automatische implementatie van software-updates:  

1. Maak een regel voor automatische implementatie waarmee implementatie-instellingen als de volgende worden opgegeven:  

   -   Doelverzameling  

   -   Bepaal of u de implementatie of rapportage over compatibiliteit van software-updates wilt inschakelen voor de clientcomputers in de doelverzameling.  

   -   Criteria voor software-updates  

   -   Evaluatie- en implementatieschema's  

   -   Gebruikerservaring  

   -   Downloadeigenschappen  

2. De software-updates worden toegevoegd aan een software-updategroep.  

3. De software-updategroep wordt geïmplementeerd naar de clientcomputers in de doelverzameling, als deze is opgegeven.  

   U moet bepalen welke implementatiestrategie er moet worden gebruikt in uw omgeving. U kunt bijvoorbeeld een regel voor automatische implementatie maken en een verzameling van testclients als doel nemen. Nadat u hebt gecontroleerd of de software-updates op de testgroep zijn geïnstalleerd, kunt u een nieuwe implementatie aan de regel toevoegen of de verzameling in de bestaande implementatie wijzigen in een doelverzameling die een grotere set van clients bevat. De software-updateobjecten die door de regels voor automatische implementatie worden gemaakt, zijn interactief.  

- Software-updates die zijn geïmplementeerd met een regel voor automatische implementatie worden automatisch geïmplementeerd voor nieuwe clients die aan de doelverzameling zijn toegevoegd.  

- Nieuwe software-updates die zijn toegevoegd aan een software-updategroep, worden automatisch geïmplementeerd naar de clients in de doelverzameling.  

- U kunt implementaties voor de regel voor automatische implementatie op elk gewenst moment in- of uitschakelen.  

  Nadat u een regel voor automatische implementatie hebt gemaakt, kunt u aanvullende implementaties aan de regel toevoegen. Dit kan helpen bij het beheren van de complexiteit van het implementeren van verschillende updates voor verschillende verzamelingen. Elke nieuwe implementatie beschikt over de volledige functionaliteit en implementatiecontrole, en elke implementatie die u toevoegt:  

- Gebruikt dezelfde bijwerkgroep en hetzelfde bijwerkpakket die worden gemaakt wanneer de ADR voor het eerst wordt uitgevoerd  

- U kunt een andere verzameling opgeven  

- Ondersteunt unieke implementatie-eigenschappen, waaronder:  

  -   Activeringstijd  

  -   Deadline  

  -   Ervaringen van eindgebruikers weergeven of verbergen  

  -   Afzonderlijke waarschuwingen voor deze implementatie  

##  <a name="software-update-deployment-process"></a><a name="BKMK_DeploymentProcess"></a>Implementatie proces voor software-updates  
 Nadat u software-updates implementeert of wanneer er een automatische implementatieregel wordt uitgevoerd en software-updates implementeert, wordt er een implementatietoewijzingsbeleid toegevoegd aan het machinebeleid voor de site. De software-updates worden naar de pakketbron gedownload vanaf de downloadlocatie, het internet of de gedeelde netwerkmap. De software-updates worden gekopieerd van de pakketbron naar de inhoudsbibliotheek op de siteserver en vervolgens gekopieerd naar de inhoudsbibliotheek op het distributiepunt.  

 Wanneer een clientcomputer in de doelverzameling voor de implementatie het machinebeleid ontvangt, start de clientagent voor software-updates een evaluatiescan. De client agent downloadt de inhoud voor vereiste software-updates van een distributie punt naar de lokale client cache op het **tijdstip waarop de software beschikbaar is** voor de implementatie en vervolgens kunnen de software-updates worden geïnstalleerd. De software-updates in optionele implementaties (implementaties zonder installatiedeadline) worden pas gedownload wanneer een gebruiker de installatie handmatig start.  

 Wanneer de geconfigureerde deadline verstrijkt, voert de clientagent voor software-updates een scan uit om te controleren of de software-updates nog steeds vereist zijn. Vervolgens wordt de lokale cache op de clientcomputer gecontroleerd en wordt er nagegaan of de bronbestanden voor de software-update nog steeds beschikbaar zijn. Tot slot installeert de client de software-updates. Als de inhoud uit de clientcache is verwijderd om ruimte vrij te maken voor een andere implementatie, downloadt de client de software-updates opnieuw vanaf het distributiepunt naar de clientcache. Software-updates worden altijd naar de clientcache gedownload, ongeacht de maximale grootte van de clientcache. Wanneer de installatie is voltooid, controleert de clientagent of de software-updates nog vereist zijn en vervolgens wordt er een statusbericht naar het beheerpunt verzonden om aan te geven dat de software-updates nu op de client zijn geïnstalleerd.  

### <a name="required-system-restart"></a>Het systeem verplicht opnieuw opstarten  
 Standaard wordt het opnieuw starten van het systeem geïnitieerd wanneer software-updates voor een vereiste implementatie op een clientcomputer worden geïnstalleerd en het opnieuw opstarten van het systeem is vereist. Voor software-updates die voor de deadline zijn geïnstalleerd, wordt het automatisch opnieuw starten van het systeem uitgesteld, totdat de deadline is bereikt, tenzij de computer voordat tijdstip om een andere reden opnieuw wordt opgestart. Het opnieuw starten van het systeem kan worden onderdrukt voor servers en werkstations. Deze instellingen worden geconfigureerd op de pagina **Gebruikerservaring** van de wizard Software-updates toepassen of de wizard voor het maken van regels voor automatische updates.  

### <a name="deployment-reevaluation-cycle"></a>Cyclus voor het opnieuw evalueren van implementaties  
 Clientcomputers starten standaard om de zeven dagen een cyclus voor het opnieuw evalueren van implementaties. Tijdens deze evaluatiecyclus controleert de clientcomputer of er software-updates aanwezig zijn die eerder zijn geïmplementeerd en geïnstalleerd. Als er software-updates ontbreken, worden de software-updates opnieuw geïnstalleerd vanuit de lokale cache. Als een software-updates niet langer beschikbaar is in de lokale cache, kan deze vanaf een distributiepunt worden gedownload en vervolgens worden geïnstalleerd. U kunt de planning voor opnieuw evalueren configureren op de pagina **Software-updates** in de clientinstellingen.  

##  <a name="support-for-windows-embedded-devices-that-use-write-filters"></a><a name="BKMK_EmbeddedDevices"></a>Ondersteuning voor Windows Embedded-apparaten die gebruikmaken van schrijf filters  
 Wanneer u software-updates implementeert voor Windows Embedded-apparaten waarvoor een schrijffilter is ingeschakeld, kunt u opgeven of het schrijffilter op het apparaat tijdens de implementatie moet worden uitgeschakeld en of het apparaat vervolgens na de implementatie opnieuw moet worden opgestart. Als het schrijffilter niet wordt uitgeschakeld, wordt de software geïmplementeerd op een tijdelijke overlay en wordt de software niet meer geïnstalleerd wanneer het apparaat opnieuw start, tenzij een andere implementatie afdwingt dat wijzigingen blijvend zijn.  

> [!NOTE]  
>  Wanneer u een software-update implementeert op een Windows Embedded-apparaat, moet u ervoor zorgen dat het apparaat lid is van een verzameling met een geconfigureerd onderhoudsvenster. U kunt op deze manier beheren wanneer het schrijffilter is uitgeschakeld en ingeschakeld en wanneer het apparaat opnieuw wordt gestart.  

 De gebruikerservaringinstelling die het gedrag van het schrijffilter bepaalt, is het selectievakje **Wijzigingen doorvoeren bij deadline of tijdens onderhoud (opnieuw opstarten noodzakelijk)**.  

 Zie [planning voor client implementatie op Windows Embedded-apparaten](../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)voor meer informatie over de manier waarop Configuration Manager Inge sloten apparaten beheert die gebruikmaken van schrijf filters.  

##  <a name="extend-software-updates-in-configuration-manager"></a><a name="BKMK_ExtendSoftwareUpdates"></a> Software-updates uitbreiden in Configuration Manager  
 Gebruik System Center Updates Publisher om software-updates te beheren die niet beschikbaar zijn via Microsoft Update. Nadat u de software-updates naar de update server hebt gepubliceerd en de software-updates in Configuration Manager hebt gesynchroniseerd, kunt u de software-updates implementeren op Configuration Manager-clients. Zie [updates publisher 2011](https://go.microsoft.com/fwlink/p/?LinkId=252947)voor meer informatie over updates Publisher.  

## <a name="next-steps"></a>Volgende stappen
[Software-updates plannen](../plan-design/plan-for-software-updates.md)
