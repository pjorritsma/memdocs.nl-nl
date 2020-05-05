---
title: Hoge beschikbaarheid
titleSuffix: Configuration Manager
description: Meer informatie over het implementeren van Configuration Manager met behulp van opties die een hoge mate van beschik bare service onderhouden.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cf8714aff7235736628d44238561eea82b896698
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073310"
---
# <a name="high-availability-options-for-configuration-manager"></a>Opties voor hoge Beschik baarheid voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel wordt beschreven hoe u Configuration Manager implementeert met behulp van opties die een hoog niveau van beschik bare service onderhouden.

De volgende Configuration Manager opties bieden ondersteuning voor hoge Beschik baarheid:

- Configureer een zelfstandige primaire site met een extra site server in de passieve modus.  

- Een SQL Server AlwaysOn-beschikbaarheids groep configureren voor de site database op primaire sites en de centrale beheer site.

- Sites ondersteunen meerdere exemplaren van site systeem rollen die belang rijke services bieden aan clients. Bijvoorbeeld beheer punten en distributie punten.  

- Centrale beheer sites en primaire sites ondersteunen de back-up van de site database. In de site database worden alle configuraties voor sites en clients opgeslagen. De sites in een hiërarchie delen deze configuratie gegevens.  

- De ingebouwde opties voor site Recovery kunnen de downtime van de server verlagen. Met deze geavanceerde opties kunt u het herstel vereenvoudigen wanneer u een hiërarchie hebt met een centrale beheer site.  

- Clients kunnen veelvoorkomende problemen automatisch oplossen zonder tussen komst van de beheerder.  

- Sites genereren waarschuwingen over clients die geen recente gegevens kunnen verzenden, waarmee beheerders worden gewaarschuwd voor potentiële problemen.  

- Configuration Manager biedt diverse ingebouwde rapporten en dash boards. U kunt deze gebruiken om problemen en trends te identificeren voordat ze problemen ondervinden voor Server-of client bewerkingen.  

Configuration Manager bevat verschillende functies die een nabije Real-Time service bieden. Als deze functies essentieel zijn om te voldoen aan uw bedrijfs vereisten, kunt u uw sites en hiërarchieën plannen en configureren voor maximale Beschik baarheid. Bijvoorbeeld:  

- [Acties voor client meldingen](../../../clients/manage/manage-clients.md), zoals opnieuw opstarten, start Windows Defender-scans of extern bureau blad.  

- Berichten op basis van status voor bewakings functies, zoals software-updates en Endpoint Protection.

- [Scripts](../../../../apps/deploy-use/create-deploy-scripts.md)

- [CMPivot](../../manage/cmpivot.md)

Andere functies van Configuration Manager geen Real-Time service bieden. Deze functies omvatten, maar zijn niet beperkt tot, client instellingen, hardware-en software-inventaris, software-implementaties en instellingen voor naleving. Verwacht dat ze met een bepaalde gegevens latentie functioneren. Het is ongebruikelijk voor de meeste scenario's waarbij een tijdelijke onderbreking van de service is vereist om een kritiek probleem te worden. Om de downtime te minimaliseren, kunt u de autonomie van bewerkingen beheren en een hoog service niveau bieden, uw sites en hiërarchieën configureren met hoge Beschik baarheid.  

Configuration Manager-clients worden bijvoorbeeld meestal autonoom uitgevoerd met behulp van bekende schema's en configuraties voor bewerkingen, en schema's voor het verzenden van gegevens naar de site voor verwerking.  

- Wanneer clients geen contact kunnen maken met de site, worden de gegevens in de cache opgeslagen voordat ze contact kunnen opnemen met de site.  

- Clients die geen verbinding kunnen maken met de site blijven werken. Ze gebruiken de laatste bekende schema's en gegevens in de cache, totdat ze contact kunnen opnemen met de site en nieuwe beleids regels ontvangen. Een client kan bijvoorbeeld een eerder gedownloade toepassing die moet worden uitgevoerd of geïnstalleerd, opslaan.

- De site bewaakt de site systemen en clients voor periodieke status updates. Het kan waarschuwingen genereren wanneer deze onderdelen niet kunnen worden geregistreerd.  

- Ingebouwde rapporten bieden inzicht in lopende bewerkingen, historische bewerkingen en huidige trends. Configuration Manager biedt ook ondersteuning voor berichten op basis van status die bijna realtime informatie bieden voor actieve bewerkingen.  


## <a name="high-availability-for-sites-and-hierarchies"></a><a name="bkmk_snh"></a>Hoge Beschik baarheid voor sites en hiërarchieën  

### <a name="use-a-site-server-in-passive-mode"></a>Een site server in de passieve modus gebruiken

Installeer een extra site server in de *passieve* modus voor een zelfstandige primaire site. De site server in de passieve modus is naast uw bestaande site server in de *actieve* modus. Een site server in de passieve modus is beschikbaar voor onmiddellijk gebruik, indien nodig. Zie [hoge Beschik baarheid van site server](site-server-high-availability.md)voor meer informatie.  

### <a name="use-a-remote-content-library"></a>Een externe inhouds bibliotheek gebruiken

Verplaats de inhouds bibliotheek van de site naar een externe locatie die Maxi maal beschik bare opslag biedt. Deze functie is vereist voor hoge Beschik baarheid van site server. Zie [de inhouds bibliotheek](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote)voor meer informatie.

### <a name="centralize-content-sources"></a>Inhouds bronnen centraliseren

Voor alle software-inhoud in Configuration Manager is een pakket bron locatie in het netwerk vereist. Gecentraliseerde en Maxi maal beschik bare opslag gebruiken om een algemene pakket bron locatie voor alle inhoud te hosten.

### <a name="use-a-sql-server-always-on-availability-group-to-host-the-site-database"></a>Een SQL Server AlwaysOn-beschikbaarheids groep gebruiken om de site database te hosten

Host de site database op primaire sites en de centrale beheer site op SQL Server AlwaysOn-beschikbaarheids groepen. Zie [SQL Server always on voor een Maxi maal beschik bare site database](sql-server-alwayson-for-a-highly-available-site-database.md)voor meer informatie.  

### <a name="use-a-sql-server-cluster-to-host-the-site-database"></a>Een SQL Server-cluster gebruiken om de site database te hosten

Wanneer u een SQL Server cluster gebruikt voor de Data Base op een centrale beheer site of primaire site, kunt u gebruikmaken van de failover-ondersteuning ingebouwd in SQL Server.  

Secundaire sites kunnen geen SQL Server cluster gebruiken en geen back-up of herstel van de site database ondersteunen. Herstel een secundaire site door de secundaire site opnieuw te installeren vanuit de bovenliggende primaire site.  

### <a name="deploy-a-hierarchy-of-sites-with-a-central-administration-site-and-one-or-more-child-primary-sites"></a>Een hiërarchie van sites met een centrale beheer site en een of meer onderliggende primaire sites implementeren

Deze configuratie kan fout tolerantie bieden wanneer uw sites overlappende segmenten van uw netwerk beheren. Daarnaast biedt het een extra herstel optie om de informatie in de gedeelde data base die beschikbaar is op een andere site te gebruiken om de site database op de herstelde site opnieuw op te bouwen. Gebruik deze optie om een mislukte of niet-beschik bare back-up van de data base van de mislukte site te vervangen.  

### <a name="create-regular-backups-at-central-administration-sites-and-primary-sites"></a>Maak regel matig back-ups op centrale beheer sites en primaire sites

Wanneer u een reguliere site back-up maakt en test, zorgt dit ervoor dat u de benodigde gegevens hebt om een site te herstellen. U kunt ook een site binnen de minimale hoeveelheid tijd herstellen.  

### <a name="install-multiple-instances-of-site-system-roles"></a>Meerdere exemplaren van site systeem rollen installeren

Wanneer u meerdere exemplaren van essentiële site systeem rollen installeert, geeft u redundante contact punten voor clients op. Meerdere beheer punten en distributie punten bieden bijvoorbeeld redundante service in het geval dat een specifieke server offline is.  

### <a name="install-multiple-instances-of-the-sms-provider-at-a-site"></a>Meerdere exemplaren van de SMS-provider installeren op een site

De SMS-provider biedt het punt van beheer contact voor een of meer Configuration Manager-consoles. Installeer meerdere SMS-providers om redundantie te bieden voor contact punten om uw site en hiërarchie te beheren.  


## <a name="high-availability-for-site-system-roles"></a><a name="bkmk_ssr"></a>Hoge Beschik baarheid voor site systeem rollen

Op elke site implementeert u site systeem rollen om de services te leveren die clients op die site moeten gebruiken. De site database bevat de configuratie gegevens voor de site en voor alle clients. Gebruik een of meer van de beschik bare opties om te voorzien in hoge Beschik baarheid van de site database en het herstel van de site en site database, indien nodig.  

### <a name="redundancy-for-important-site-system-roles"></a>Redundantie voor belang rijke site systeem rollen

- Application Catalog-webservicepunt  

- Application catalog-website punt  

- Distributiepunt  

- Beheerpunt  

- Software-updatepunt  

- Statusmigratiepunt  

Om redundantie te bieden voor rapportage over sites en clients, installeert u meerdere exemplaren van het Reporting Services-punt.

Voor failover-ondersteuning met het software-update punt gebruikt u Windows Power shell om deze functie te installeren op een NLB-cluster (Windows Network Load Balancing).  

### <a name="built-in-site-backup"></a>Ingebouwde site back-up

Configuration Manager bevat een ingebouwde back-uptaak om u te helpen bij het maken van een back-up van uw site en essentiële gegevens volgens een regel matig schema. Daarnaast ondersteunt de Configuration Manager-installatie wizard site herstel acties om u te helpen bij het herstellen van een site naar bewerkingen.  

### <a name="publishing-to-active-directory-domain-services-and-dns"></a>Publiceren naar Active Directory Domain Services en DNS

Configureer elke site om gegevens over de site te publiceren naar Active Directory Domain Services en DNS. Met deze publicatie kunnen clients de meest toegankelijke server op het netwerk identificeren. Clients gebruiken deze ook om te bepalen wanneer nieuwe site systeem servers beschikbaar zijn voor het leveren van belang rijke Services, zoals beheer punten.  

### <a name="sms-provider-and-configuration-manager-console"></a>SMS-provider en Configuration Manager-console

Configuration Manager ondersteunt het installeren van meerdere SMS-providers op afzonderlijke servers als meerdere toegangs punten voor de-console. Als één SMS-provider server offline is, kunt u nog steeds sites en clients weer geven en beheren.  

Wanneer een Configuration Manager-console verbinding maakt met een site, maakt deze verbinding met een exemplaar van de SMS-provider op die site. Het exemplaar van de SMS-provider is wille keurig geselecteerd. Als de geselecteerde SMS-provider niet beschikbaar is, hebt u de volgende opties:  

- Verbind de console opnieuw met de-site. Elke nieuwe verbindings aanvraag krijgt wille keurig een exemplaar van de SMS-provider toegewezen. Het is mogelijk dat de nieuwe verbinding een beschikbaar exemplaar krijgt toegewezen.  

- Verbind de console met een andere Configuration Manager site en beheer de configuratie vanuit die verbinding. Met deze optie wordt een lichte vertraging in configuratie wijzigingen van niet meer dan een paar minuten geïntroduceerd. Nadat de SMS-provider voor de site online is, sluit u de Configuration Manager-console rechtstreeks aan op de site die u wilt beheren.  

Installeer de Configuration Manager-console op meerdere computers voor gebruik door beheerders. Elke SMS-provider ondersteunt verbindingen van meer dan één console.  

### <a name="management-point"></a>Beheerpunt

Installeer meerdere beheer punten op elke primaire site en schakel de sites in om site gegevens te publiceren naar uw Active Directory-infra structuur en naar DNS.  

Meerdere beheer punten helpen bij het verdelen van het gebruik van één beheer punt door meerdere clients. Overweeg ook een of meer database replica's voor beheer punten te installeren. Deze configuratie vermindert de processorintensieve bewerkingen van het beheer punt. Ook wordt de beschik baarheid van deze essentiële site systeemrol verhoogd.  

Secundaire sites ondersteunen alleen installatie van één beheer punt, dat zich op de secundaire site server bevindt. Beheer punten op secundaire sites worden niet beschouwd als een Maxi maal beschik bare configuratie.  

> [!NOTE]  
> Apparaten die worden beheerd door on-premises Mobile Device Management verbinding maken met slechts één beheer punt op een primaire site. Het beheer punt wordt tijdens de inschrijving toegewezen door Configuration Manager aan het mobiele apparaat en verandert vervolgens niet. Wanneer u meerdere beheer punten installeert en meer dan één voor mobiele apparaten inschakelt, is het beheer punt dat is toegewezen aan een mobiele apparaat-client niet-deterministisch.  
>
> Als het beheer punt dat een client voor mobiele apparaten gebruikt, niet beschikbaar is, moet u het probleem met dat beheer punt oplossen of het mobiele apparaat wissen en het mobiele apparaat opnieuw registreren, zodat het kan worden toegewezen aan een operationeel beheer punt dat is ingeschakeld voor mobiele apparaten.  

### <a name="distribution-point"></a>Distributiepunt

Installeer meerdere distributie punten en implementeer inhoud op meerdere distributie punten. Voeg meer dan één distributie punt per grens groep toe om ervoor te zorgen dat clients verschillende opties in hun inhouds aanvraag krijgen. Configureer de relaties tussen grens groepen zo dat ze een predicable terugval gedrag hebben op een andere grens groep of een Cloud distributiepunt. Zie [grens groepen configureren](boundary-groups.md)voor meer informatie.  

### <a name="application-catalog-web-service-point-and-application-catalog-website-point"></a>Application Catalog-webservicepunt en Application catalog-website punt

> [!Important]
> De Silverlight-gebruikers ervaring van de toepassings catalogus wordt niet ondersteund vanaf de huidige branch-versie 1806. Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  
>
> Raadpleeg voor meer informatie de volgende artikelen:
>
> - [Software Center configureren](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Verwijderde en afgeschafte functies](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Installeer meer dan één exemplaar van elke site systeemrol. Voor de beste prestaties implementeert u een van beide op dezelfde site systeem server.  

Elke Application Catalog-site systeemrol biedt dezelfde informatie als andere exemplaren van die rol, ongeacht de locatie in de hiërarchie. Wanneer een client een aanvraag doet voor de toepassings catalogus en u hebt geconfigureerd dat clients automatisch het standaard Application catalog-website punt detecteren, wordt de client omgeleid naar een beschikbaar exemplaar. Clients geven de voor keur aan lokale toepassings catalogus exemplaren op basis van de huidige netwerk locatie van de client.  

Zie de client instellingen van de [computer agent](../../../clients/deploy/about-client-settings.md#computer-agent) voor meer informatie over deze client instelling en de werking van automatische detectie.  


## <a name="high-availability-for-clients"></a><a name="bkmk_client"></a>Hoge Beschik baarheid voor clients  

### <a name="client-operations-are-autonomous"></a>Client bewerkingen zijn autonoom

Configuration Manager-client autonomie omvat het volgende gedrag:  

- Clients hebben geen doorlopende contact met specifieke site systeem servers nodig. Ze gebruiken bekende configuraties om vooraf geconfigureerde acties volgens een schema uit te voeren.  

- Clients kunnen elk beschikbaar exemplaar van een site systeemrol gebruiken dat services biedt aan clients. Ze proberen contact op te nemen met bekende servers tot ze een beschik bare server hebben gevonden.  

- Clients kunnen inventarisatie, software-implementaties en vergelijk bare geplande acties uitvoeren, onafhankelijk van direct contact met site systeem servers.  

- Clients die zijn geconfigureerd voor het gebruik van een terugval status punt kunnen gegevens verzenden naar het terugval status punt wanneer ze niet kunnen communiceren met een beheer punt.  

### <a name="clients-can-repair-themselves"></a>Clients kunnen zichzelf herstellen

Clients herstellen automatisch meest voorkomende problemen zonder directe administratieve interventie.  

- Periodiek evalueren clients zelf hun status. Ze ondervinden veelvoorkomende problemen door gebruik te maken van een lokale cache met herstels tappen en bron bestanden voor reparaties.  

- Wanneer een client geen status gegevens naar de site kan verzenden, kan de site een waarschuwing genereren. Gebruikers met beheerders rechten die deze waarschuwingen ontvangen, kunnen direct actie ondernemen om de normale werking van de client te herstellen.  

### <a name="clients-cache-information-to-use-in-the-future"></a>Clients slaan gegevens in de cache op voor gebruik in de toekomst

Wanneer een client communiceert met een beheer punt, kan de client de volgende gegevens verkrijgen en in de cache opslaan:  

- Clientinstellingen  

- Client schema's  

- Informatie over software-implementaties en een down load van de software waarvan de client is gepland, wanneer de implementatie is geconfigureerd voor deze actie.  

Wanneer een client geen contact kan maken met een beheer punt, worden de status-, status-en client gegevens die ze rapporteren aan de site lokaal in de cache opgeslagen door de clients. De client verzendt deze gegevens nadat er contact is gemaakt met een beheer punt.  

### <a name="client-can-submit-status-to-a-fallback-status-point"></a>Client kan status verzenden naar een terugval status punt

Wanneer u een client configureert om een terugval status punt te gebruiken, geeft u een aanvullend contact punt op voor de client om belang rijke informatie over de werking ervan te verzenden. Clients die zijn geconfigureerd voor het gebruik van een terugval status punt blijven status over hun bewerkingen verzenden naar die site systeemrol, zelfs wanneer de client niet kan communiceren met een beheer punt.  

### <a name="central-management-of-client-data-and-client-identity"></a>Centraal beheer van client gegevens en client identiteit

De site database, in plaats van de afzonderlijke client, behoudt belang rijke informatie over de identiteit van elke client en koppelt die gegevens aan een specifieke computer of gebruiker.  

- De bron bestanden van de client op een computer kunnen worden verwijderd en opnieuw worden geïnstalleerd zonder dat dit van invloed is op de historische records voor de computer waarop de-client is geïnstalleerd.  

- Een storing van een client computer heeft geen invloed op de integriteit van de gegevens die in de Data Base zijn opgeslagen. Deze informatie kan beschikbaar blijven voor rapportage.  


## <a name="options-for-sites-and-site-system-roles-that-arent-highly-available"></a><a name="bkmk_nonHAoptions"></a>Opties voor sites en site systeem rollen die niet Maxi maal beschikbaar zijn

Verschillende site systemen bieden geen ondersteuning voor meerdere exemplaren op een site of in de hiërarchie. Deze informatie kan u helpen bij de voor bereiding voor deze site systemen die offline gaan.  

### <a name="asset-intelligence-synchronization-point-hierarchy"></a>Asset Intelligence-synchronisatie punt (hiërarchie)

Deze site systeemrol wordt niet beschouwd als bedrijfs kritiek en biedt optionele functionaliteit in Configuration Manager. Als dit site systeem offline gaat, gebruikt u een van de volgende opties:  

- Verhelp de reden voor het offline zetten van het site systeem.  

- Verwijder de rol van de huidige server en installeer de functie op een nieuwe server.  

### <a name="endpoint-protection-point-hierarchy"></a>Endpoint Protection-punt (hiërarchie)

Deze site systeemrol wordt niet beschouwd als bedrijfs kritiek en biedt optionele functionaliteit in Configuration Manager. Als dit site systeem offline gaat, gebruikt u een van de volgende opties:  

- Verhelp de reden voor het offline zetten van het site systeem.  

- Verwijder de rol van de huidige server en installeer de functie op een nieuwe server.  

### <a name="enrollment-point-site"></a>Inschrijvings punt (site)

Deze site systeemrol wordt niet beschouwd als bedrijfs kritiek en biedt optionele functionaliteit in Configuration Manager. Als dit site systeem offline gaat, gebruikt u een van de volgende opties:  

- Verhelp de reden voor het offline zetten van het site systeem.  

- Verwijder de rol van de huidige server en installeer de functie op een nieuwe server.  

### <a name="enrollment-proxy-point-site"></a>Inschrijvings proxy punt (site)

Deze site systeemrol wordt niet beschouwd als bedrijfs kritiek en biedt optionele functionaliteit in Configuration Manager. U kunt echter meerdere exemplaren van deze site systeemrol op een site en op meerdere sites in de hiërarchie installeren. Als dit site systeem offline gaat, gebruikt u een van de volgende opties:  

- Verhelp de reden voor het offline zetten van het site systeem.  

- Verwijder de rol van de huidige server en installeer de functie op een nieuwe server.  

Als u meer dan één inschrijvings proxy server in een-site hebt, gebruikt u een DNS-alias voor de server naam. Wanneer u deze configuratie gebruikt, biedt DNS round robin een aantal fout tolerantie en taak verdeling voor wanneer gebruikers hun mobiele apparaten inschrijven.  

### <a name="fallback-status-point-site-or-hierarchy"></a>Terugval status punt (site of hiërarchie)

Deze site systeemrol wordt niet beschouwd als bedrijfs kritiek en biedt optionele functionaliteit in Configuration Manager. Als dit site systeem offline gaat, gebruikt u een van de volgende opties:  

- Verhelp de reden voor het offline zetten van het site systeem.  

- Verwijder de rol van de huidige server en installeer de functie op een nieuwe server. Omdat aan clients het terugval status punt wordt toegewezen tijdens de client installatie, moet u bestaande clients wijzigen voor het gebruik van de nieuwe site systeem server.  

### <a name="service-connection-point-hierarchy"></a>Service verbindings punt (hiërarchie)

Hoewel deze site systeemrol kritiek is om Configuration Manager huidige vertakking up-to-date te houden, wordt het doorgaans niet vaak gebruikt. Als dit systeem offline gaat, gebruikt u een van de volgende opties:

- Verhelp de reden voor het offline zetten van het site systeem.  

- Verwijder de rol van de huidige server en installeer de functie op een nieuwe server.  


## <a name="see-also"></a>Zie ook

- [Ondersteunde configuraties](../../../plan-design/configs/supported-configurations.md)  

- [Aanbevolen hardware](../../../plan-design/configs/recommended-hardware.md)  

- [Ondersteunde besturingssystemen voor sitesysteemservers](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)

- [Vereisten voor sites en sitesystemen](../../../plan-design/configs/site-and-site-system-prerequisites.md)  

- [Gevolgen van sitefouten](../../manage/site-failure-impacts.md)  
