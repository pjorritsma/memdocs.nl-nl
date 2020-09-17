---
title: Software-updates plannen
titleSuffix: Configuration Manager
description: Een plan voor de infra structuur van het software-update punt is essentieel voordat u software-updates gebruikt in een Configuration Manager-productie omgeving.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/16/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
ms.openlocfilehash: c38f3b509ba6104647dd60c8284fde52b5b4995e
ms.sourcegitcommit: 6176a7825d6c663faa318a6818b7764bc70f08fc
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/17/2020
ms.locfileid: "90718821"
---
# <a name="plan-for-software-updates-in-configuration-manager"></a>Software-updates plannen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voordat u software-updates in een Configuration Manager productie omgeving gebruikt, is het belang rijk dat u het plannings proces door lopen. Een goed plan voor de infra structuur van het software-update punt is essentieel voor een geslaagde implementatie van software-updates. Zie [grootte en schaal getallen](../../core/plan-design/configs/size-and-scale-numbers.md#software-update-point)voor informatie over capaciteits planning voor software-updates.


##  <a name="determine-the-software-update-point-infrastructure"></a><a name="BKMK_SUPInfrastructure"></a> De infra structuur van het software-update punt bepalen  

Deze sectie bevat de volgende subonderwerpen:    
- [Lijst met software-update punten](#BKMK_SUPList)
- [Wisseling van software-update punt](#BKMK_SUPSwitching)
- [Clients hand matig overschakelen naar een nieuw software-update punt](#BKMK_ManuallySwitchSUPs)
- [Software-updatepunten in een niet-vertrouwd forest](#BKMK_SUP_CrossForest)
- [Een bestaande WSUS-server gebruiken als synchronisatie bron op de site op het hoogste niveau](#BKMK_WSUSSyncSource)
- [Software-update punt op een secundaire site](#BKMK_SUPSecSite)  
- [Plannen voor clients op Internet](#bkmk_internet-clients)  
- [Inhoud van software-updates plannen](#bkmk_content)  
- [Plan voor updates van derden](#bkmk_thirdparty)  


De centrale beheer site en alle onderliggende primaire sites moeten een software-update punt hebben. Bepaal bij het plannen van de software-update punt infrastructuur de volgende afhankelijkheden:
- Waar het software-update punt voor de site moet worden geïnstalleerd  
- Voor welke sites is een software-update punt vereist dat communicatie van clients op internet accepteert
- Of u nu een software-update punt op secundaire sites nodig hebt  

> [!IMPORTANT]  
>  Zie [vereisten voor software-updates](prerequisites-for-software-updates.md)voor meer informatie over de interne en externe afhankelijkheden die zijn vereist voor software-updates.  

Voeg meerdere software-update punten toe aan een Configuration Manager primaire site om fout tolerantie te bieden. Het failover-ontwerp van het software-update punt wijkt af van het zuivere wille keurig model dat wordt gebruikt in het ontwerp voor beheer punten. In tegens telling tot het ontwerp van beheer punten, zijn er kosten voor client-en netwerk prestaties in het ontwerp van software-update punten wanneer clients overschakelen naar een nieuw software-update punt. Wanneer de client overschakelt naar een nieuwe WSUS-server voor software-updates, is het resultaat een stijging van de catalogusgrootte en van de gekoppelde vereisten van clients en netwerkprestaties. Daarom bewaart de client affiniteit met het laatste software-update punt van waaruit het is gescand.  

Het eerste software-updatepunt dat u installeert op een primaire site is de synchronisatiebron voor alle bijkomende software-updatepunten die u toevoegt aan de primaire site. Nadat u software-update punten hebt toegevoegd en synchronisatie hebt gestart, bekijkt u de status van de software-update punten en de synchronisatie bron van het knoop punt **synchronisatie status van software-update punt** in de werk ruimte **bewaking** .  

Als er een fout is opgetreden in het software-update punt dat is geconfigureerd als de synchronisatie bron voor de site, verwijdert u de mislukte rol hand matig. Selecteer vervolgens een nieuw software-update punt om te gebruiken als synchronisatie bron. Zie [een site Systeemrol verwijderen](../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#bkmk_role)voor meer informatie.  


###  <a name="software-update-point-list"></a><a name="BKMK_SUPList"></a> Lijst met software-updatepunten  

Configuration Manager voorziet de client van een lijst met software-update punten in de volgende scenario's:  

- Een nieuwe client ontvangt het beleid om software-updates in te scha kelen  

- Een client kan geen verbinding maken met het toegewezen software-update punt en moet overschakelen naar een ander  

De client selecteert wille keurig een software-update punt uit de lijst. Hiermee wordt prioriteit gegeven aan de software-update punten in hetzelfde forest. Configuration Manager voorziet clients van een andere lijst, afhankelijk van het type client:  

-   **Clients op het intranet**: ontvangen een lijst met software-update punten die u kunt configureren om verbindingen alleen via het intranet toe te staan, of een lijst met software-update punten die client verbindingen via internet en intranet toestaan.  

-   **Clients op Internet**: ontvangen een lijst met software-update punten die u configureert om verbindingen alleen via Internet toe te staan, of een lijst met software-update punten die client verbindingen via internet en intranet toestaan.  


###  <a name="software-update-point-switching"></a><a name="BKMK_SUPSwitching"></a> Overschakeling tussen software-updatepunten  

> [!NOTE]  
> Clients gebruiken grens groepen om een nieuw software-update punt te vinden. Als hun huidige software-update punt niet meer toegankelijk is, gebruiken ze ook grens groepen om een nieuwe te vinden. Voeg afzonderlijke software-update punten toe aan verschillende grens groepen om te bepalen welke servers door een client kunnen worden gevonden. Zie [Software-update punten](../../core/servers/deploy/configure/boundary-groups.md#bkmk_sup)voor meer informatie.  

Als u meerdere software-update punten op een site hebt en één mislukt of niet beschikbaar is, zullen clients verbinding maken met een ander software-update punt. Met deze nieuwe server blijven clients scannen op de nieuwste software-updates. Wanneer een client voor het eerst een software-update punt krijgt toegewezen, blijft deze toegewezen aan dat software-update punt, tenzij het scannen niet kan worden uitgevoerd.  

De scan naar software-updates kan mislukken met een aantal verschillende retry- en non-retry-foutcodes. Als de scan niet kan worden uitgevoerd en er een retry-foutcode wordt gegeven, start de client een nieuwe poging om te scannen naar software-updates op het software-updatepunt. De omstandigheden die leiden tot een retry-foutcode, zijn doorgaans te wijten aan het niet beschikbaar zijn van de WSUS-server of aan een tijdelijke overbelasting ervan. Wanneer de client niet kan scannen op software-updates, gebruikt deze het volgende proces:  

1.  De client scant naar software-updates:  
    - Op het geplande tijdstip
    - Wanneer het hand matig wordt uitgevoerd vanuit het configuratie scherm op de client
    - Wanneer het hand matig wordt uitgevoerd vanuit de Configuration Manager-console via een actie voor client meldingen
    - Wanneer het wordt uitgevoerd vanuit een Configuration Manager SDK-methode  

2.  Als de scan mislukt, wacht de client 30 minuten om de scan opnieuw uit te voeren. Het gebruikt hetzelfde software-update punt.  

3.  De client voert mini maal vier keer om de 30 minuten opnieuw een poging uit. Na de vierde fout, en nadat er nog twee minuten zijn gewacht, gaat de client naar het volgende software-update punt in de lijst.  

4.  De client herhaalt dit proces met het nieuwe software-update punt. Na een geslaagde scan blijft de client verbinding maken met het nieuwe software-update punt.  

De volgende lijst bevat aanvullende informatie voor het opnieuw proberen en overschakelen van scenario's voor software-update punten:  

-   Als een client geen verbinding heeft met het intranet en niet kan scannen op software-updates, wordt het niet overgeschakeld naar een ander software-update punt. Deze fout wordt verwacht, omdat de client het interne netwerk of een software-update punt dat verbindingen van het intranet toestaat niet kan bereiken. De Configuration Manager-client bepaalt de beschik baarheid van het intranet software-update punt.  

-   Als u clients beheert op internet en meerdere software-update punten hebt geconfigureerd om communicatie van clients op het Internet te accepteren, volgt het switch proces het standaard proces voor nieuwe pogingen dat eerder is beschreven.  

-   Als het scan proces wordt gestart, maar de-client is uitgeschakeld voordat de scan is voltooid, wordt deze niet beschouwd als een scan fout en wordt deze niet geteld als een van de vier nieuwe pogingen.  

Wanneer Configuration Manager een van de volgende Windows Update fout codes voor agents ontvangt, probeert de client de verbinding te verbreken:  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

Als u de betekenis van een fout code wilt opzoeken, converteert u de decimale fout code naar hexadecimaal en zoekt u naar de hexadecimale waarde op een site, zoals de [Windows Update Agent-fout codes wiki](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx). de decimale fout code 2149842970 is bijvoorbeeld hexadecimaal 8024001A. Dit betekent dat WU_E_POLICY_NOT_SET een beleids waarde niet is ingesteld.  


###  <a name="manually-switch-clients-to-a-new-software-update-point"></a><a name="BKMK_ManuallySwitchSUPs"></a> Clients hand matig overschakelen naar een nieuw software-update punt

Configuration Manager-clients overschakelen naar een nieuw software-update punt wanneer er problemen zijn met het actieve software-update punt. Deze wijziging treedt alleen op wanneer een client meerdere software-update punten ontvangt van een beheer punt.

> [!IMPORTANT]    
> Wanneer u apparaten overschakelt om een nieuwe server te gebruiken, gebruiken de apparaten terugval om die nieuwe server te vinden. Clients scha kelen naar het nieuwe software-update punt tijdens de volgende scan cyclus voor software-updates.<!-- SCCMDocs#1537 -->
>
> Voordat u met deze wijziging begint, moet u de configuratie van de grens groep controleren om ervoor te zorgen dat uw software-update punten zich in de juiste grens groepen bevinden. Zie [Software-update punten](../../core/servers/deploy/configure/boundary-groups.md#bkmk_sup)voor meer informatie.  
>
> Als u overschakelt naar een nieuw software-update punt, wordt extra netwerk verkeer gegenereerd. De hoeveelheid verkeer is afhankelijk van de WSUS-configuratie-instellingen, bijvoorbeeld de gesynchroniseerde classificaties en producten, of het gebruik van een gedeelde WSUS-data base. Als u van plan bent meerdere apparaten te scha kelen, kunt u overwegen tijdens onderhouds Vensters. Deze tijds duur vermindert de invloed van uw netwerk wanneer clients scannen met het nieuwe software-update punt.  

#### <a name="process-to-switch-software-update-points"></a>Proces voor het scha kelen tussen software-update punten  
Start deze wijziging op een verzameling apparaten. Nadat de clients zijn geactiveerd, zoeken ze naar een ander software-update punt bij de volgende scan.  

1.  Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en selecteer het knoop punt **Apparaatsets** .  

2.  Selecteer de doel verzameling. Klik op het tabblad **Start** van het lint in de groep **verzameling** op **client melding**en klik vervolgens op **overschakelen naar het volgende software-update punt**.  


###  <a name="software-update-points-in-an-untrusted-forest"></a><a name="BKMK_SUP_CrossForest"></a> Software-update punten in een niet-vertrouwd forest  

Maak een of meer software-update punten op een site ter ondersteuning van clients in een niet-vertrouwd forest. Als u een software-update punt in een ander forest wilt toevoegen, moet u eerst een WSUS-server in dat forest installeren en configureren. Start vervolgens de wizard om een Configuration Manager site server toe te voegen met de site systeemrol van het software-update punt. Configureer de volgende instellingen in de wizard om verbinding te maken met WSUS in het niet-vertrouwde forest:  

-   Geef een **site systeem installatie account** op dat toegang heeft tot de WSUS-server in het niet-vertrouwde forest.  

-   Geef een **WSUS-server verbindings account** op om verbinding te maken met de WSUS-server.  

U kunt bijvoorbeeld primaire site hebben in forest A met twee software-updatepunten (SUP01 en SUP02).‎ Voor dezelfde primaire site hebt u ook twee software-update punten (SUP03 en SUP04) in forest B. Wanneer u overschakelt naar het volgende software-update punt, krijgen de clients prioriteit voor de servers uit hetzelfde forest.  


###  <a name="use-an-existing-wsus-server-as-the-synchronization-source-at-the-top-level-site"></a><a name="BKMK_WSUSSyncSource"></a> Een bestaande WSUS-server gebruiken als synchronisatie bron op de site op het hoogste niveau  

Doorgaans wordt de site op het hoogste niveau van uw hiërarchie geconfigureerd om de metagegevens van software-updates te synchroniseren met Microsoft Update. Wanneer het beveiligings beleid van uw organisatie niet toestaat dat de site op het hoogste niveau toegang heeft tot internet, configureert u de synchronisatie bron voor de site op het hoogste niveau voor het gebruik van een bestaande WSUS-server. Deze WSUS-server bevindt zich niet in uw Configuration Manager-hiërarchie. U hebt bijvoorbeeld een WSUS-server in een netwerk met Internet verbinding (DMZ), maar uw site op het hoogste niveau bevindt zich in een intern netwerk zonder Internet toegang. Configureer de WSUS-server in de DMZ als uw synchronisatie bron voor de meta gegevens van software-updates. Configureer de WSUS-server in de DMZ om software-updates te synchroniseren met de criteria die u nodig hebt in Configuration Manager. Anders is het mogelijk dat de site op het hoogste niveau de software-updates die u verwacht, niet kan synchroniseren. Wanneer u het software-update punt installeert, configureert u een WSUS-server verbindings account. Dit account moet toegang hebben tot de WSUS-server in het DMZ. Controleer ook of de firewall verkeer toestaat voor de juiste poorten. Zie de [poorten die worden gebruikt door het software-update punt voor de synchronisatie bron](../../core/plan-design/hierarchy/ports.md#BKMK_PortsSUP-WSUS)voor meer informatie.  


###  <a name="software-update-point-on-a-secondary-site"></a><a name="BKMK_SUPSecSite"></a> Software-updatepunt op een secundaire Site  

Het software-updatepunt is optioneel op een secundaire site. Installeer slechts één software-update punt op een secundaire site. Wanneer een software-update punt niet is geïnstalleerd op de secundaire site, gebruiken apparaten binnen de grenzen van een secundaire site een software-update punt op hun toegewezen primaire site. Doorgaans installeert u een software-update punt op een secundaire site wanneer er een beperkte netwerk bandbreedte is tussen de apparaten in de secundaire site en de software-update punten op de bovenliggende primaire site. U kunt deze configuratie ook gebruiken wanneer het software-update punt op de primaire site de capaciteits limiet nadert. Nadat u een software-update punt op de secundaire site hebt geïnstalleerd en geconfigureerd, wordt een beleid voor de hele site bijgewerkt voor clients en beginnen ze het nieuwe software-update punt te gebruiken.  


### <a name="plan-for-internet-based-clients"></a><a name="bkmk_internet-clients"></a> Plannen voor clients op Internet

Als u apparaten wilt beheren die uw netwerk naar het Internet roamen, ontwikkelt u een plan voor het beheren van software-updates op deze apparaten. Configuration Manager ondersteunt verschillende technologieën voor dit scenario. Gebruik één of een combi natie als dat nodig is om te voldoen aan de vereisten van uw organisatie.

#### <a name="cloud-management-gateway"></a>Cloudbeheergateway
Maak een Cloud beheer gateway in Microsoft Azure en schakel ten minste één on-premises software-update punt in om verkeer toe te staan van clients op internet. Wanneer clients naar het Internet roamen, blijven ze controleren op basis van uw software-update punten. Alle clients op Internet ontvangen altijd inhoud van de Microsoft Update-Cloud service. 

Zie voor meer informatie [plannen van de Cloud beheer gateway](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) en het [configureren van grens groepen](../../core/servers/deploy/configure/boundary-groups.md#bkmk_sup).  

#### <a name="internet-based-client-management"></a>Clientbeheer via internet
Plaats een software-update punt in een Internet gericht netwerk en schakel dit in om verkeer toe te staan van clients op internet. Wanneer clients naar het Internet zwerven, scha kelen ze naar dit software-update punt voor het scannen. Alle clients op Internet ontvangen altijd inhoud van de Microsoft Update-Cloud service.

Zie [clients op Internet beheren](../../core/clients/manage/manage-clients-internet.md)voor meer informatie over de voor-en nadelen van client beheer op internet.

#### <a name="windows-update-for-business"></a>Windows Update voor Bedrijven
Met Windows Update voor bedrijven kunt u Windows 10-apparaten altijd up-to-date houden met de nieuwste updates voor kwaliteit en onderdelen. Deze apparaten maken rechtstreeks verbinding met de Windows Update Cloud service. Configuration Manager kan onderscheid maken tussen Windows 10-computers die gebruikmaken van WUfB en WSUS voor het ophalen van software-updates.

Zie [integratie met Windows Update voor bedrijven](../deploy-use/integrate-windows-update-for-business-windows-10.md)voor meer informatie.


### <a name="plan-software-update-content"></a><a name="bkmk_content"></a> Inhoud van software-updates plannen

Clients moeten de inhouds bestanden voor software-updates downloaden om ze te kunnen installeren. Configuration Manager biedt verschillende technologieën ter ondersteuning van het beheer en de levering van deze inhoud. Of configureer software-update-implementaties zodat clients rechtstreeks vanuit de Microsoft Update Cloud service inhoud kunnen ophalen.

#### <a name="download-and-distribute-content"></a>Inhoud downloaden en distribueren 
Het software-update beheer proces in Configuration Manager maakt standaard gebruik van de ingebouwde functies voor inhouds beheer. Deze functies omvatten de gecentraliseerde opslag inhouds bibliotheek met één exemplaar en het gedistribueerde ontwerp van de site systeemrol van het distributie punt. U gebruikt deze functies wanneer u software-update-implementatie pakketten downloadt en distribueert. 

Zie [software-updates downloaden](../deploy-use/download-software-updates.md)voor meer informatie.

#### <a name="manage-express-installation-files-for-windows-10"></a>Bestanden voor snelle installatie voor Windows 10 beheren
Configuration Manager ondersteunt het gebruik van bestanden voor snelle installatie voor Windows 10-updates. Bestanden voor snelle updates en ondersteunende technologieën zoals Delivery Optimization kunnen de netwerk impact van bestanden met grote inhoud die naar clients worden gedownload, verminderen. 

Zie [Windows 10 update delivery](../deploy-use/optimize-windows-10-update-delivery.md)voor meer informatie.

#### <a name="clients-download-content-from-the-internet"></a>Clients downloaden inhoud van Internet
Wanneer u software-updates op clients implementeert, configureert u de implementatie voor clients om inhoud te downloaden van de Microsoft Update-Cloud service. Wanneer clients geen inhoud van een andere inhouds bron kunnen downloaden, kunnen ze de inhoud nog steeds downloaden van het internet. 

Vanaf versie 1806 hoeft u geen implementatie pakket te maken wanneer u software-updates implementeert. Wanneer u de optie **geen implementatie pakket** selecteert, kunnen clients nog steeds inhoud downloaden van lokale bronnen, indien beschikbaar, maar meestal downloaden van de Microsoft Update-service.<!--1357933-->

Op internet gebaseerde clients downloaden altijd inhoud van de Microsoft Update-Cloud service. Distribueer geen software-update-implementatie pakketten naar een Cloud distributiepunt. Er worden kosten in rekening gebracht voor opslag met het Cloud distributiepunt, maar clients downloaden deze pakketten niet. 


### <a name="plan-for-third-party-updates"></a><a name="bkmk_thirdparty"></a> Plan voor updates van derden
Configuration Manager integreert met WSUS, dat systeem eigen ondersteuning biedt voor software-updates die zijn gepubliceerd door micro soft. De meeste klanten gebruiken andere toepassingen van derden die ook updates nodig hebben. Er zijn verschillende opties waarmee u rekening moet houden voor het up-to-date houden van toepassingen van derden.

#### <a name="supersede-applications-to-update"></a>Toepassingen die moeten worden bijgewerkt vervangen
Gebruik een vervangings relatie met de functie toepassings beheer in Configuration Manager om bestaande toepassingen bij te werken of te vervangen. Wanneer u een toepassing vervangt, moet u een nieuw implementatie type opgeven om het implementatie type van de vervangen toepassing te vervangen. Bepaal ook of u de vervangen toepassing wilt upgraden of verwijderen voordat de vervangende toepassing wordt geïnstalleerd.

Zie [toepassingen herzien en vervangen](../../apps/deploy-use/revise-and-supersede-applications.md)voor meer informatie.

#### <a name="third-party-software-updates"></a>Software-updates van derden
Vanaf versie 1806 kunt u het knoop punt **Software-update catalogi van derden** gebruiken in de Configuration Manager-console om u te abonneren op catalogi van derden, hun updates te publiceren op het software-update punt en vervolgens te implementeren op clients.<!--1352101-->

Zie [software-updates](../deploy-use/third-party-software-updates.md)van derden voor meer informatie.

#### <a name="system-center-updates-publisher"></a>System Center Updates Publisher
System Center Updates Publisher (SCUP gemaakt) is een zelfstandig hulp programma waarmee onafhankelijke software leveranciers of ontwikkel aars van line-of-business-toepassingen aangepaste updates kunnen beheren. Deze updates omvatten die met afhankelijkheden, zoals Stuur Programma's en update bundels.

Zie [System Center updates Publisher](../tools/updates-publisher.md)voor meer informatie.



##  <a name="plan-for-software-update-point-installation"></a><a name="BKMK_SUPInstallation"></a> Installatie van software-update punt plannen  

Deze sectie bevat de volgende subonderwerpen:  
- [Vereisten voor het software-updatepunt](#BKMK_SUPSystemRequirements)
- [Planning voor de installatie van WSUS](#BKMK_PlanningForWSUS)
- [Firewalls configureren](#BKMK_ConfigureFirewalls)  


Deze sectie bevat informatie over de stappen die u moet uitvoeren om de installatie van het software-update punt goed te plannen en voor te bereiden. Voordat u een site systeemrol voor het software-update punt in Configuration Manager maakt, moet u rekening houden met verschillende vereisten. De specifieke vereisten zijn afhankelijk van uw Configuration Manager-infra structuur. Wanneer u het software-update punt configureert om te communiceren met behulp van HTTPS, is deze sectie vooral belang rijk om te controleren. Voor servers met HTTPS-functionaliteit moeten extra stappen worden uitgevoerd.  

###  <a name="requirements-for-the-software-update-point"></a><a name="BKMK_SUPSystemRequirements"></a> Vereisten voor het software-update punt  

Installeer de rol van het software-update punt op een site systeem dat voldoet aan de minimum vereisten voor WSUS en de ondersteunde configuraties voor Configuration Manager-site systemen.  

-   Zie [aandachtspunten en systeem vereisten](/windows-server/administration/windows-server-update-services/plan/plan-your-wsus-deployment#11-review-considerations-and-system-requirements)voor meer informatie over de minimale vereisten voor de WSUS-serverrol in Windows Server.  

-   Zie [site-en site systeem vereisten](../../core/plan-design/configs/site-and-site-system-prerequisites.md)voor meer informatie over de ondersteunde configuraties voor Configuration Manager-site systemen.  


###  <a name="plan-for-wsus-installation"></a><a name="BKMK_PlanningForWSUS"></a> Installatie van WSUS plannen  

Installeer een ondersteunde versie van WSUS op alle site systeem servers die u configureert voor de rol software-update punt. Wanneer u het software-update punt niet op de site server installeert, installeert u de WSUS-beheer console op de site server. Met dit onderdeel kan de site server communiceren met WSUS die wordt uitgevoerd op het software-update punt.  

Wanneer u WSUS op Windows Server 2012 of hoger gebruikt, moet u extra machtigingen configureren om het **WSUS-Configuration Manager** onderdeel in Configuration Manager toe te staan om verbinding te maken met WSUS. Met dit onderdeel worden periodieke status controles uitgevoerd. Kies een van de volgende opties om de vereiste machtiging te configureren:  

-   Voeg de **SYSTEM** -account toe aan de **WSUS-administrators** -groep  

-   Voeg het **NT AUTHORITY\SYSTEM** -account toe als een gebruiker voor de WSUS-data base (SUSDB). Configureer een minimum van het webService-databaserol lidmaatschap.  
  
Zie [de WSUS](/windows-server/administration/windows-server-update-services/deploy/1-install-the-wsus-server-role)-serverrol installeren voor meer informatie over het installeren van WSUS op Windows Server.  

Wanneer u meer dan één software-updatepunt op een primaire site installeert, gebruikt u dezelfde WSUS-database voor elk software-updatepunt in hetzelfde Active Directory-forest. Als u dezelfde data base deelt, worden de prestaties verbeterd wanneer clients overschakelen naar een nieuw software-update punt. Zie [een gedeelde WSUS-Data Base voor software-update punten gebruiken](software-updates-best-practices.md#bkmk_shared-susdb)voor meer informatie.  

#### <a name="configuring-the-wsus-content-directory-path"></a>Het pad naar de map WSUS-inhoud configureren

Wanneer u WSUS installeert, moet u een pad naar een inhoudsmap opgeven. De WSUS-inhoudsmap wordt voornamelijk gebruikt voor het opslaan van de bestanden voor de micro soft-Software licentievoorwaarden die tijdens het scannen nodig zijn voor clients. De Configuration Manager de map met WSUS-inhoud mag niet overlappen met uw inhouds bron directory voor Configuration Manager software-implementatie pakketten. Het overlappen van de inhoud van de WSUS-map en de bron van het Configuration Manager-pakket leidt ertoe dat onjuiste bestanden worden verwijderd uit de map WSUS-inhoud.

####  <a name="configure-wsus-to-use-a-custom-website"></a><a name="BKMK_CustomWebSite"></a> WSUS configureren voor het gebruik van een aangepaste website  
Wanneer u WSUS installeert, hebt u de optie de bestaande IIS Standaard website te gebruiken of een aangepaste WSUS-website te maken. Maak een aangepaste website voor WSUS, zodat de WSUS-Services door IIS worden gehost op een speciale virtuele website. Anders deelt deze dezelfde website die wordt gebruikt door de andere Configuration Manager-site systemen of-toepassingen. Deze configuratie is met name nodig wanneer u de rol van het software-update punt op de site server installeert. Wanneer u WSUS uitvoert in Windows Server 2012 of hoger, wordt WSUS standaard geconfigureerd om poort 8530 te gebruiken voor HTTP en poort 8531 voor HTTPS. Geef deze poorten op wanneer u het software-update punt op een site maakt.  


####  <a name="use-an-existing-wsus-infrastructure"></a><a name="BKMK_WSUSInfrastructure"></a> Een bestaande WSUS-infra structuur gebruiken  
Selecteer een WSUS-server die actief was in uw omgeving voordat u Configuration Manager als een software-update punt hebt geïnstalleerd. Wanneer het software-update punt is geconfigureerd, geeft u de synchronisatie-instellingen op. Configuration Manager maakt verbinding met de WSUS-server die op de software-update punt server wordt uitgevoerd en configureert WSUS met dezelfde instellingen. 

Voordat u de server als een software-update punt configureert, moet u de configuratie voor de producten en classificaties vergelijken met de instellingen van uw Configuration Manager. Als u de bestaande WSUS-server hebt gesynchroniseerd voordat u deze configureert als een software-update punt en de lijsten met producten en classificaties verschillen, worden alle meta gegevens van software-updates gesynchroniseerd, ongeacht de geconfigureerde instellingen. Dit gedrag resulteert in onverwachte meta gegevens van software-updates in de site database. 

U ondervindt hetzelfde gedrag wanneer u producten of classificaties rechtstreeks toevoegt in de WSUS-beheer console en vervolgens onmiddellijk een synchronisatie initieert. Standaard worden elk uur dat Configuration Manager verbinding maakt met WSUS en worden alle instellingen die buiten Configuration Manager zijn gewijzigd, opnieuw ingesteld. De software-updates die niet voldoen aan de producten en classificaties die u opgeeft in de synchronisatie-instellingen, worden ingesteld op verlopen. Vervolgens worden ze verwijderd uit de site database.  

Wanneer een WSUS-server is geconfigureerd als een software-update punt, kunt u deze niet meer gebruiken als zelfstandige WSUS-server. Als u een afzonderlijke zelfstandige WSUS-server nodig hebt die niet wordt beheerd door Configuration Manager, configureert u deze op een andere server.  

####  <a name="configure-wsus-as-a-replica-server"></a><a name="BKMK_WSUSAsReplica"></a> WSUS configureren als een replicaserver  
Wanneer u de rol van het software-update punt op een primaire site server toevoegt, kunt u geen WSUS-server gebruiken die als een replica is geconfigureerd. Wanneer de WSUS-server is geconfigureerd als een replica, kan Configuration Manager de WSUS-server niet configureren en mislukt de WSUS-synchronisatie. Het eerste software-updatepunt dat u installeert op een primaire site wordt het standaardsoftware-updatepunt. Andere software-updatepunten op de site zijn geconfigureerd als replica's van het standaardsoftware-updatepunt.  

####  <a name="decide-whether-to-configure-wsus-to-use-ssl"></a><a name="BKMK_WSUSandSSL"></a> Beslissen of WSUS moet worden geconfigureerd voor het gebruik van SSL  

Het SSL-protocol gebruiken om het software-update punt te beveiligen, wordt sterk aanbevolen. WSUS gebruikt SSL om clientcomputers en downstream-WSUS-servers voor de WSUS-server te verifiëren. WSUS gebruikt ook SSL om de metagegevens van de software-update te versleutelen. Wanneer u ervoor kiest om WSUS met SSL te beveiligen, moet u de WSUS-server voorbereiden voordat u het software-update punt installeert.

Wanneer u het software-update punt installeert en configureert, selecteert u de optie om **SSL-communicatie voor de WSUS-server in te scha kelen**. Als dat niet het geval is, wordt WSUS door Configuration Manager geconfigureerd om SSL niet te gebruiken. Wanneer u SSL inschakelt op een software-update punt, moet u ook software-update punten op onderliggende sites configureren voor het gebruik van SSL. Zie voor meer informatie de [zelf studie een software-update punt configureren voor het gebruik van TLS/SSL met een PKI-certificaat](../get-started/software-update-point-ssl.md).

###  <a name="configure-firewalls"></a><a name="BKMK_ConfigureFirewalls"></a> Firewalls configureren  

Het software-update punt op een Configuration Manager centrale beheer site communiceert met WSUS op het software-update punt. WSUS communiceert met de synchronisatie bron om meta gegevens van software-updates te synchroniseren. Software-update punten op een onderliggende site communiceren met het software-update punt op de bovenliggende site. Wanneer er meer dan één software-update punt op een primaire site is, communiceren de extra software-update punten met het standaard software-update punt. De standaardrol is het eerste software-update punt dat op de site is geïnstalleerd.  

Mogelijk moet u de firewall configureren om het HTTP-of HTTPS-verkeer toe te staan dat door WSUS wordt gebruikt in de volgende scenario's: 
- Tussen het software-update punt en het Internet
- Tussen een software-update punt en de synchronisatie bron stroomopwaarts
- Tussen extra software-update punten  

De verbinding met Microsoft Update is altijd geconfigureerd om poort 80 te gebruiken voor HTTP en poort 443 voor HTTPS. Gebruik een aangepaste poort voor de verbinding van WSUS op het software-update punt op een onderliggende site naar WSUS op het software-update punt op de bovenliggende site. Gebruik de export-en import synchronisatie methode wanneer uw beveiligings beleid de verbinding niet toestaat. Zie de sectie [synchronisatie bron](#BKMK_SyncSource) in dit artikel voor meer informatie. Voor meer informatie over de poorten die worden gebruikt door WSUS, raadpleegt [u hoe u kunt bepalen welke poort instellingen worden gebruikt door WSUS in Configuration Manager](../get-started/install-a-software-update-point.md#wsus-settings).  


#### <a name="restrict-access-to-specific-domains"></a>Toegang tot specifieke domeinen beperken  

Als uw organisatie netwerk communicatie met Internet beperkt met behulp van een firewall of proxy apparaat, moet u het actieve software-update punt toestaan om toegang te krijgen tot internet-eind punten. WSUS en Automatische updates kunnen communiceren met de Microsoft Update-Cloud service.

Zie [vereisten voor Internet toegang](../../core/plan-design/network/internet-endpoints.md#bkmk_sum)voor meer informatie.


##  <a name="plan-for-synchronization-settings"></a><a name="BKMK_SyncSettings"></a> Planning voor synchronisatie-instellingen  

Deze sectie bevat de volgende subonderwerpen:  
- [Synchronisatie bron](#BKMK_SyncSource)
- [Synchronisatie planning](#BKMK_SyncSchedule)
- [Updateclassificaties](#BKMK_UpdateClassifications)
- [Producten](#BKMK_UpdateProducts)
- [Vervangingsregels](#BKMK_SupersedenceRules)
- [Talen](#BKMK_UpdateLanguages)  
- [Maximale uitvoerings tijd](#bkmk_maxruntime)


De synchronisatie van software-updates in Configuration Manager downloadt de meta gegevens van software-updates op basis van de criteria die u configureert. De site op het hoogste niveau in uw hiërarchie synchroniseert software-updates van Microsoft Update. U hebt de optie om het software-update punt op de site op het hoogste niveau te configureren om te synchroniseren met een bestaande WSUS-server, niet in de Configuration Manager-hiërarchie. De onderliggende primaire sites synchroniseren metagegevens van software-updates van het software-updatepunt op de centrale beheersite. Voordat u een software-updatepunt installeert en configureert, moet u deze sectie gebruiken om te plannen voor de synchronisatie-instellingen.  


###  <a name="synchronization-source"></a><a name="BKMK_SyncSource"></a> Synchronisatiebron  

De synchronisatie bron instellingen voor het software-update punt geven de locatie op waar het software-update punt meta gegevens van software-updates ophaalt. Ook wordt aangegeven of het synchronisatie proces WSUS-rapportage gebeurtenissen maakt.  

-   **Synchronisatie bron**: standaard configureert het software-update punt op de site op het hoogste niveau de synchronisatie bron voor Microsoft Update. U hebt de optie de site op het hoogste niveau met een bestaande WSUS-server te synchroniseren. Het software-update punt op een onderliggende primaire site configureert de synchronisatie bron als het software-update punt op de centrale beheer site.  

    -  Het eerste software-updatepunt dat u installeert op een primaire site, dat het standaardsoftware-updatepunt is, synchroniseert met de centrale beheersite. Extra software-upatepunten aan de primaier site synchroniseren met het standaardsoftware-updatepunt aan de primaire site.  

    - Wanneer een software-update punt niet is verbonden met Microsoft Update of van de upstream-update server, moet u de synchronisatie bron configureren om niet te synchroniseren met een geconfigureerde synchronisatie bron. In plaats daarvan configureert u deze voor het gebruik van de export-en import functie van het hulp programma **wsusutil** om software-updates te synchroniseren. Zie de sectie [Software-updates synchroniseren vanaf een niet-verbonden software-updatepunt](../get-started/synchronize-software-updates-disconnected.md)voor meer informatie.  

-   **WSUS-rapportage gebeurtenissen:** De Windows Update-Agent op client computers kan gebeurtenis berichten maken voor WSUS-rapportage. Deze gebeurtenissen worden niet gebruikt door Configuration Manager. Daarom is de optie, **geen WSUS-rapportage gebeurtenissen maken**standaard geselecteerd. Wanneer deze gebeurtenissen niet worden gemaakt, is de enige keer dat de client verbinding moet maken met de WSUS-server tijdens de evaluatie van software-updates en compatibiliteits scans. Als deze gebeurtenissen nodig zijn voor rapportage buiten Configuration Manager, wijzigt u deze instelling om WSUS-rapportage gebeurtenissen te maken.  


###  <a name="synchronization-schedule"></a><a name="BKMK_SyncSchedule"></a> Synchronisatie planning  

Configureer de synchronisatie planning alleen op het software-update punt op de site op het hoogste niveau in de Configuration Manager-hiërarchie. Wanneer u de synchronisatieplanning configureert, synchroniseert het software-updatepunt met de synchronisatiebron op de datum en tijd die u hebt opgegeven. Met de aangepaste planning kunt u software-updates synchroniseren om te optimaliseren voor uw omgeving. Houd rekening met de prestatie vereisten van de WSUS-server, site server en het netwerk. 2:00 bijvoorbeeld eenmaal per week. U kunt ook de synchronisatie hand matig starten op de site op het hoogste niveau met behulp van de actie **synchronisatie software-updates** van de knoop punten **alle software-updates** of **Software-Update groepen** in de Configuration Manager-console.  

> [!TIP]  
>  Plan de synchronisatie van software-updates om uit te voeren met een tijd die geschikt is voor uw omgeving. Een veelvoorkomend scenario is het instellen van het synchronisatie schema om uit te voeren kort na de reguliere software-update van micro soft op de tweede dinsdag van elke maand. Deze dag wordt doorgaans *patch dinsdag*genoemd. Als u Configuration Manager gebruikt voor het leveren van Endpoint Protection en Windows Defender-definitie-en engine-updates, kunt u de synchronisatie planning instellen om dagelijks te worden uitgevoerd.  

Nadat het software-update punt met succes is gesynchroniseerd, verzendt het een synchronisatie aanvraag naar onderliggende sites. Als u aanvullende software-update punten op een primaire site hebt, verzendt het een synchronisatie aanvraag naar elk software-update punt. Dit proces wordt herhaald op elke site in de hiërarchie.  


###  <a name="update-classifications"></a><a name="BKMK_UpdateClassifications"></a> Update classificaties  

Elke software-update wordt gedefinieerd met een updateclassificatie die helpt de verschillende types updates te organiseren. Tijdens het synchronisatie proces worden de meta gegevens voor de opgegeven classificaties gesynchroniseerd met de site. 

Configuration Manager ondersteunt de synchronisatie van de volgende update classificaties:  

-   **Essentiële updates**: een in grote mate vrijgegeven update voor een specifiek probleem dat betrekking heeft op een kritieke bug die niet aan beveiliging voldoet.  

-   **Definitie-updates**: een update voor virus-of andere definitie bestanden.  

-   **Feature packs**: nieuwe product functies die zijn gedistribueerd buiten een product release en die gewoonlijk zijn opgenomen in de volgende volledige product release.  

-   **Beveiligings updates**: een ruim vrijgegeven update voor een productspecifiek, beveiligings probleem.  

-   **Service packs**: een cumulatieve set hotfixes die wordt toegepast op een besturings systeem of toepassing. Deze hotfixes omvatten beveiligings updates, essentiële updates en software-updates.  

-   **Hulpprogram ma's**: een hulp programma of functie waarmee u een of meer taken kunt volt ooien.  

-   **Update pakketten**: een cumulatieve set met hotfixes die samen zijn verpakt voor een eenvoudige implementatie. Deze hotfixes omvatten beveiligings updates, essentiële updates en software-updates. Een updatepakket gaat in het algemeen over een specifiek gebied, zoals beveiliging of een productcomponent.  

-   **Updates**: een update voor een toepassing of bestand dat momenteel is geïnstalleerd.  

-   **Upgrades**: een functie update naar een nieuwe versie van Windows 10.  

Configureer de update classificatie-instellingen alleen op de site op het hoogste niveau. De update classificatie-instellingen zijn niet geconfigureerd op het software-update punt op onderliggende sites, omdat de meta gegevens van de software-updates worden gerepliceerd van de site op het hoogste niveau. Wanneer u de update classificaties selecteert, Let er dan op hoe meer classificaties u selecteert, hoe langer het duurt om de meta gegevens van software-updates te synchroniseren.  

> [!WARNING]  
>  Wis als best practice alle classificaties voordat u voor de eerste keer synchroniseert. Na de initiële synchronisatie selecteert u de gewenste classificaties en voert u de synchronisatie opnieuw uit.  


###  <a name="products"></a><a name="BKMK_UpdateProducts"></a> Producten  

De meta gegevens voor elke software-update definiëren een of meer producten waarvoor de update van toepassing is. Een product is een specifieke editie van een besturings systeem of toepassing. Een voor beeld van een product is micro soft Windows 10. Een product familie is het basis besturingssysteem of de toepassing van waaruit de afzonderlijke producten zijn afgeleid. Een voor beeld van een product familie is micro soft Windows, waarvan Windows 10 en Windows Server 2016 lid zijn. Selecteer een product familie of individuele producten binnen een product familie.  

Wanneer software-updates van toepassing zijn op meerdere producten, en ten minste een van de producten is geselecteerd voor synchronisatie, worden alle producten weer gegeven in de Configuration Manager-console, zelfs als sommige producten niet zijn geselecteerd. U kunt bijvoorbeeld alleen het product Windows Server 2012 selecteren. Als een software-update van toepassing is op Windows Server 2012 en Windows Server 2012 Data Center Edition, zijn beide producten in de site database.  

Configureer de product instellingen alleen op de site op het hoogste niveau. De product instellingen worden niet geconfigureerd op het software-update punt voor onderliggende sites, omdat de meta gegevens van de software-updates worden gerepliceerd van de site op het hoogste niveau. Hoe meer producten u selecteert, hoe langer het duurt om de meta gegevens van software-updates te synchroniseren.  

> [!IMPORTANT]  
>  Configuration Manager slaat een lijst van producten en product families op waaruit u kunt kiezen wanneer u het software-update punt voor het eerst installeert. Producten en product families die zijn vrijgegeven nadat Configuration Manager is uitgebracht, zijn mogelijk niet beschikbaar om te selecteren tot u de synchronisatie hebt voltooid. Het synchronisatie proces werkt de lijst met beschik bare producten en product families bij waaruit u kunt kiezen. Wis alle producten voordat u software-updates voor de eerste keer synchroniseert. Na de initiële synchronisatie selecteert u de gewenste producten en voert u de synchronisatie opnieuw uit.  


###  <a name="supersedence-rules"></a><a name="BKMK_SupersedenceRules"></a> Vervangings regels  

Een software-updat die een andere software-update vervangt, doet gewoonlijk een of meerdere van de volgende acties:  

-   Bevordert, verbetert of werkt de oplossing bij die werd geleverd door een of meerdere eerder vrijgegeven updates.  

-   Verbetert de efficiëntie van het vervangen update bestands pakket, dat wordt geïnstalleerd op clients als de update is goedgekeurd voor installatie. De vervangen update kan bijvoorbeeld bestanden bevatten die niet langer relevant zijn voor de oplossing of voor de besturings systemen die worden ondersteund door de nieuwe update. Deze bestanden zijn niet opgenomen in het vervangende bestands pakket van de update.  

-   Werkt nieuwere versies van het product bij. Met andere woorden, het werkt versies bij die niet langer toepasselijk zijn voor oudere versies of configuraties van een product. Updates kunnen ook andere updates vervangen als er wijzigingen zijn aangebracht om taalondersteuning uit te breiden. Een latere revisie van een product update voor Microsoft 365-apps kan bijvoorbeeld de ondersteuning voor een ouder besturings systeem verwijderen, maar dit kan extra ondersteuning bieden voor nieuwe talen in de initiële update release.  

Geef in de eigenschappen voor het software-update punt op dat de vervangen software-updates onmiddellijk verlopen zijn. Deze instelling voor komt dat ze worden opgenomen in nieuwe implementaties. Ook worden de bestaande implementaties gemarkeerd om aan te geven dat ze een of meer verlopen software-updates bevatten. Of geef een periode op voordat de vervangen software-updates zijn verlopen. Met deze actie kunt u de implementatie voortzetten. 

Denk eens aan de volgende scenario's waarin u een vervangen software-update moet implementeren:  

-   Een vervangende software-update ondersteunt alleen nieuwere versies van een besturings systeem. Op sommige van uw client computers worden eerdere versies van het besturings systeem uitgevoerd.  

-   Een vervangende software-update heeft een beperktere toepas baarheid dan de software-update die deze vervangt. Dit gedrag zou het voor sommige clients ongeschikt maken.  

-   Als een vervangende software-update niet is goedgekeurd voor implementatie in uw productie omgeving.  

    > [!NOTE]  
    > - Voor Configuration Manager versie 1806, wanneer Configuration Manager een vervangen software-update instelt op **verlopen**, wordt de update niet ingesteld op **geweigerd** in WSUS. Clients blijven scannen op een verlopen update totdat de update hand matig of via een aangepast script wordt geweigerd.  Na de Configuration Manager versie 1806, worden door Configuration Manager ook de vervangen updates in WSUS geweigerd. Zie [onderhoud van software-updates](../deploy-use/software-updates-maintenance.md)voor meer informatie over de WSUS-opschoon taak.
    > - Vanaf Configuration Manager versie 1810 kunt u het gedrag van de vervangings regels voor **onderdeel updates** afzonderlijk van **updates zonder onderdelen**opgeven.

###  <a name="languages"></a><a name="BKMK_UpdateLanguages"></a> Talen  

Met de taal instellingen voor het software-update punt kunt u het volgende configureren: 
- De talen waarvoor de samenvattings gegevens (meta gegevens van software-updates) zijn gesynchroniseerd voor software-updates  
- De software-update bestands talen die worden gedownload voor software-updates  

#### <a name="software-update-file"></a>Software-updatebestand  
Configureer talen voor de instelling van het **Software-update bestand** in de eigenschappen voor het software-update punt. Deze instelling biedt de standaard talen die beschikbaar zijn wanneer u software-updates op een site downloadt. Wijzig de talen die standaard worden geselecteerd wanneer de software-updates worden gedownload of geïmplementeerd. Tijdens het downloadproces worden de software-updatebestanden voor de geconfigureerde talen gedownload naar de bronlocatie van het implementatiepakket, als de software-updatebestanden beschikbaar zijn in de geselecteerde taal. Vervolgens worden ze gekopieerd naar de inhouds bibliotheek op de site server. Vervolgens worden ze gedistribueerd naar de distributie punten die zijn geconfigureerd voor het pakket.  

Configureer de taal instellingen voor het software-update bestand met de talen die het vaakst worden gebruikt in uw omgeving. Clients in uw site gebruiken bijvoorbeeld voornamelijk Engels en Japans voor Windows of toepassingen. Er zijn nog enkele andere talen die op de site worden gebruikt. Selecteer in de kolom **Software-update bestand** de optie alleen Engels en Japans wanneer u de software-update downloadt of implementeert. Met deze actie kunt u de standaard instellingen gebruiken op de pagina **taal selecteren** van de wizards implementatie en downloaden. Deze actie voor komt ook dat overbodige update bestanden worden gedownload. Configureer deze instelling op elk software-update punt in de hiërarchie van Configuration Manager.  



#### <a name="summary-details"></a>Overzichtsgegevens  
Tijdens het synchronisatieproces wordt de informatie bij de overzichtsgegevens (metagegevens van software-updates) bijgewerkt voor software-updates in de talen die u opgeeft. De meta gegevens bevatten informatie over de software-update, bijvoorbeeld:
- Naam
- Beschrijving
- Producten die de update ondersteunt
- Update classificatie
- Artikel-ID
- URL downloaden
- Toepasselijkheidsregels

Configureer de instellingen voor de samenvattings informatie alleen op de site op het hoogste niveau. De overzichts gegevens zijn niet geconfigureerd op het software-update punt op onderliggende sites, omdat de meta gegevens van de software-updates worden gerepliceerd van de centrale beheer site door gebruik te maken van replicatie op basis van een bestand. Wanneer u de talen voor de overzichtsgegevens selecteert, selecteert u alleen de talen die u in uw omgeving nodig hebt. Hoe meer talen u selecteert, hoe langer het duurt om de metagegevens van software-updates te synchroniseren. Configuration Manager geeft de meta gegevens van software-updates weer in de land instellingen van het besturings systeem waarin de Configuration Manager-console wordt uitgevoerd. Als de gelokaliseerde eigenschappen voor de software-updates niet beschikbaar zijn in de land instellingen van dit besturings systeem, wordt de informatie over software-updates in het Engels weer gegeven.  

> [!IMPORTANT]  
>  Selecteer alle beknopte overzichts gegevens talen die u nodig hebt. Wanneer het software-update punt op de site op het hoogste niveau synchroniseert met de synchronisatie bron, bepalen de geselecteerde overzichts gegevens talen welke meta gegevens van de software-updates worden opgehaald. Als u de overzichts gegevens talen wijzigt nadat de synchronisatie ten minste één keer is uitgevoerd, worden de meta gegevens van software-updates voor de gewijzigde overzichts gegevens talen alleen voor nieuwe of bijgewerkte software-updates opgehaald. De software-updates die al zijn gesynchroniseerd, worden niet bijgewerkt met nieuwe meta gegevens voor de gewijzigde talen, tenzij er een wijziging is aangebracht in de software-update op de synchronisatie bron.


###  <a name="maximum-run-time"></a><a name="bkmk_maxruntime"></a> Maximale uitvoerings tijd
<!--3734426-->
*(Geïntroduceerd in versie 1906)*

Vanaf versie 1906 kunt u de maximale hoeveelheid tijd opgeven dat de installatie van een software-update moet worden voltooid. U kunt de maximale uitvoerings tijd opgeven voor het volgende:

- **Maximale uitvoerings tijd voor updates van Windows-onderdelen (minuten)**
  - **Onderdeel updates** : een update in een van deze drie classificaties
    - Uitvoeren
    - Updatepakketten
    - Servicepacks

- **Maximale uitvoerings tijd voor updates van Office 365 en niet-onderdelen voor Windows (minuten)**
  - **Updates zonder onderdelen** : een update die geen functie-upgrade is en waarvan het product wordt vermeld als een van de volgende:
    - Windows 10 (alle versies)
    - Windows Server 2012
    - Windows Server 2012 R2
    - Windows Server 2016
    - Windows Server 2019
    - Office 365

- Deze instellingen wijzigen alleen de maximale runtime voor nieuwe updates die worden gesynchroniseerd vanuit Microsoft Update. Hiermee wordt de uitvoerings tijd niet gewijzigd voor bestaande onderdelen of updates die geen onderdeel zijn.
- Alle andere producten en classificaties kunnen met deze instelling niet worden geconfigureerd. Als u de maximale uitvoerings tijd van een van deze updates wilt wijzigen, [configureert u de instellingen voor software-updates](../get-started/manage-settings-for-software-updates.md#BKMK_SoftwareUpdatesSettings)

> [!NOTE]
> In versie 1906 is de maximale runtime niet beschikbaar wanneer u het software-update punt op het hoogste niveau installeert. Na de installatie bewerkt u de maximale uitvoerings tijd op het software-update punt op het hoogste niveau.

##  <a name="plan-for-a-software-updates-maintenance-window"></a><a name="BKMK_MaintenanceWindow"></a> Een onderhouds venster voor software-updates plannen  

Een onderhouds venster toevoegen dat specifiek is voor de installatie van software-updates. Met deze actie kunt u een algemeen onderhouds venster en een ander onderhouds venster voor software-updates configureren. Wanneer u zowel een algemeen onderhouds venster als een onderhouds venster voor software-updates configureert, installeren clients software-updates alleen tijdens het onderhouds venster voor software-updates. 

Vanaf Configuration Manager versie 1810 kunt u dit gedrag wijzigen en de installatie van software-updates toestaan tijdens een algemeen onderhouds venster. Zie [client instellingen voor software-updates](../../core/clients/deploy/about-client-settings.md#bkmk_SUMMaint)voor meer informatie over deze client instelling.

Zie [onderhouds Vensters gebruiken](../../core/clients/manage/collections/use-maintenance-windows.md)voor meer informatie over onderhouds Vensters.  


##  <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a> Opties voor het opnieuw opstarten van Windows 10-clients na de installatie van een software-update

Wanneer een software-update die opnieuw moet worden opgestart, wordt geïmplementeerd en geïnstalleerd met behulp van Configuration Manager, plant de client een in behandeling zijnde opnieuw opstarten en wordt het dialoog venster opnieuw opstarten weer gegeven.

Wanneer het opnieuw opstarten in behandeling is voor een Configuration Manager software-update, is de optie voor **bijwerken en opnieuw opstarten** en **bijwerken en afsluiten** beschikbaar op Windows 10-computers in de Windows-energie opties. Nadat u een van deze opties hebt gebruikt, wordt het dialoog venster voor opnieuw opstarten niet weer gegeven nadat de computer opnieuw is opgestart. In bepaalde gevallen kan het besturings systeem de opties voor opnieuw opstarten in behandeling verwijderen. Dit kan gebeuren als de functie snel opstarten in Windows 10 is ingeschakeld. Zie [updates kunnen niet worden geïnstalleerd met snel opstarten in Windows 10](https://support.microsoft.com/help/4011287/windows-updates-not-install-with-fast-startup)voor meer informatie.

## <a name="evaluate-software-updates-after-a-servicing-stack-update"></a><a name="bkmk_ssu"></a> Software-updates evalueren na een onderhouds stack-update
<!--4639943-->
Met ingang van versie 2002 detecteert Configuration Manager of een onderhouds stack-update (SSU) deel uitmaakt van een installatie voor meerdere updates. Wanneer een SSU wordt gedetecteerd, wordt het eerst geïnstalleerd. Na de installatie van de SSU wordt een evaluatie cyclus voor software-updates uitgevoerd om de resterende updates te installeren. Met deze wijziging kan een afhankelijke cumulatieve update worden geïnstalleerd na de onderhouds stack-update. Het apparaat hoeft niet opnieuw te worden opgestart tussen installaties en u hoeft geen extra onderhouds venster te maken. SSUs worden eerst alleen geïnstalleerd voor installaties die niet door de gebruiker zijn gestart. Als een gebruiker bijvoorbeeld een installatie voor meerdere updates vanuit software Center initieert, wordt de SSU mogelijk niet eerst geïnstalleerd. De installatie van SSUs is voor het eerst niet beschikbaar voor Windows Server-besturings systemen wanneer u Configuration Manager versie 2002. <!--7813007-->Deze functionaliteit is toegevoegd aan Configuration Manager versie 2006 voor Windows Server-besturings systemen.



## <a name="next-steps"></a>Volgende stappen
Wanneer u software-updates hebt gepland, raadpleegt u [voorbereiden op het beheer van software-updates](../get-started/prepare-for-software-updates-management.md).  

Zie voor meer informatie over het beheren van Windows als een service [basis principes van Configuration Manager als een service en Windows als een service](../../core/understand/configuration-manager-and-windows-as-service.md).