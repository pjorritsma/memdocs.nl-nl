---
title: Site bronnen zoeken
titleSuffix: Configuration Manager
description: Meer informatie over hoe en wanneer Configuration Manager-clients service locatie gebruiken om site resources te vinden.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ae72df4b-5f5d-4e19-9052-bda28edfbace
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 262234edbd6fac6973653ca6cac62853fde23b2d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700109"
---
# <a name="learn-how-clients-find-site-resources-and-services-for-configuration-manager"></a>Meer informatie over hoe clients site bronnen en-services vinden voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager-clients gebruiken een proces dat *service locatie* wordt genoemd om site systeem servers te vinden waarmee ze kunnen communiceren en die services bieden die clients gebruiken. Informatie over hoe en wanneer clients service locatie gebruiken om site bronnen te vinden, kunnen u helpen bij het configureren van uw sites voor het ondersteunen van client taken. Deze configuraties kunnen vereisen dat de site communiceert met domein-en netwerk configuraties als Active Directory Domain Services (AD DS) en DNS. U kunt er ook voor zorgen dat u complexere alternatieven moet configureren.  

Voor beelden van site systeem rollen die services bieden zijn:

- De kern site systeem server voor clients.
- Het beheer punt.
- Aanvullende site systeem servers waarmee de client kan communiceren, zoals distributie punten en software-update punten.  



##  <a name="fundamentals-of-service-location"></a><a name="bkmk_fund"></a> Basis principes van service locatie  
 Een client evalueert de huidige netwerk locatie, de voor keur voor het communicatie protocol en de toegewezen site wanneer de service locatie wordt gebruikt om een beheer punt te vinden waarmee kan worden gecommuniceerd.  

**Een client communiceert met een beheer punt tot:**  
- Down load informatie over andere beheer punten voor de site, zodat deze een lijst met bekende beheer punten (ook wel de *MP-lijst*genoemd) kan maken voor toekomstige service locatie cycli.  
- Upload configuratie details, zoals inventaris en status.  
- Down load een beleid dat configuraties op de client instelt en de client van software kan informeren dat het kan of moet worden geïnstalleerd, en andere gerelateerde taken.  
- Vraag informatie op over aanvullende site systeem rollen die services leveren die de client heeft geconfigureerd voor gebruik. Voor beelden zijn onder andere distributie punten voor software die de client kan installeren, of een software-update punt waarvan updates moeten worden opgehaald.  

**Een Configuration Manager-client maakt een service locatie aanvraag:**  
- Elke 25 uur van een doorlopende bewerking.  
- Wanneer de client een wijziging in de netwerk configuratie of-locatie detecteert.  
- Wanneer de **ccmexec.exe** -service op de computer (de kern client service) wordt gestart.  
- Wanneer de client een site systeemrol moet vinden die een vereiste service levert.  

**Wanneer een client probeert servers te vinden die site systeem rollen hosten**, gebruikt deze service locatie om een site systeemrol te vinden die het client protocol (http of https) ondersteunt. Standaard gebruiken clients de meest beveiligde methode die voor hen beschikbaar is. Overweeg de volgende:  

- U moet een PKI (Public Key Infrastructure) hebben en u moet PKI-certificaten installeren op clients en servers om HTTPS te gebruiken. Zie [PKI-certificaat vereisten voor Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md)voor meer informatie over het gebruik van certificaten.  

- Wanneer u een sitesysteemrol implementeert die gebruikmaakt van Internet Information Services (IIS) en communicatie van clients ondersteunt, moet u opgeven of clients verbinding met het sitesysteem maken via HTTP of HTTPS. Als u HTTP gebruikt, dient u ook opties voor ondertekening en versleuteling te overwegen. Zie voor meer informatie  [planning voor ondertekening en versleuteling](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) in de [Beveiliging plannen](../../../core/plan-design/security/plan-for-security.md).  

##  <a name="service-location-and-how-clients-determine-their-assigned-management-point"></a><a name="BKMK_Plan_Service_Location"></a> Service locatie en hoe clients hun toegewezen beheer punt bepalen  
Wanneer een client voor het eerst wordt toegewezen aan een primaire site, wordt er een standaard beheer punt voor die site geselecteerd. Primaire sites bieden ondersteuning voor meerdere beheer punten en elke client identificeert onafhankelijk een beheer punt als het standaard beheer punt. Dit standaard beheer punt wordt dan het toegewezen beheer punt van de client. (U kunt ook client installatie opdrachten gebruiken om het toegewezen beheer punt voor een client in te stellen wanneer deze wordt geïnstalleerd.)  

Een client selecteert een beheer punt om mee te communiceren op basis van de huidige netwerk locatie en grens groeps configuraties van de client. Hoewel er een beheer punt aan is toegewezen, is dit mogelijk niet het beheer punt dat door de client wordt gebruikt.  

> [!NOTE]  
> Een client gebruikt het toegewezen beheerpunt altijd voor registratieberichten en bepaalde beleidsberichten, zelfs wanneer andere berichten worden verzonden naar een proxybeheerpunt of lokaal beheerpunt.

U kunt voorkeursbeheerpunten gebruiken. Voorkeurs beheer punten zijn beheer punten van de toegewezen site van een client die zijn gekoppeld aan een grens groep die de client gebruikt om site systeem servers te vinden. De koppeling van een voorkeurs beheer punt met een grens groep als een site systeem server is vergelijkbaar met de manier waarop distributie punten of status migratie punten zijn gekoppeld aan een grens groep. Als u voorkeursbeheerpunten voor de hiërarchie inschakelt, zal een client die een beheerpunt van de toegewezen site gebruikt, proberen eerst een voorkeursbeheerpunt te gebruiken voordat andere beheerpunten worden gebruikt.  

U kunt ook de informatie in de blog van het [affiniteit van beheer punten](/archive/blogs/jchalfant/management-point-affinity-added-in-configmgr-2012-r2-cu3) gebruiken om de affiniteit van het beheer punt te configureren. Beheer punt affiniteit overschrijft het standaard gedrag voor toegewezen beheer punten en stelt de client in staat om een of meer specifieke beheer punten te gebruiken.  

Telkens wanneer een client contact moet opnemen met een beheer punt, wordt de MP-lijst gecontroleerd, die lokaal wordt opgeslagen in Windows Management Instrumentation (WMI). De client maakt een initiële MP-lijst wanneer deze wordt geïnstalleerd. De client werkt de lijst vervolgens regel matig bij met details over elk beheer punt in de hiërarchie.  

Wanneer de client geen geldig beheer punt kan vinden in de MP-lijst, zoekt het naar de volgende service locatie bronnen, in de juiste volg orde, totdat er een beheer punt wordt gevonden dat kan worden gebruikt:  

1.  Beheerpunt  
2.  AD DS  
3.  DNS  
4.  WINS  

Nadat een client een beheer punt heeft gevonden en contact maakt, wordt de huidige lijst met beschik bare beheer punten in de hiërarchie gedownload en wordt de lokale MP-lijst bijgewerkt. Dit geldt ook voor clients die lid zijn van een domein en voor clients die dat niet zijn.  

Wanneer een Configuration Manager-client die zich op Internet bevindt bijvoorbeeld verbinding maakt met een beheer punt op internet, stuurt het beheer punt die client een lijst met beschik bare beheer punten op internet in de site. Op deze manier ontvangen clients in een domein of werkgroep ook de lijst met beheerpunten die mogelijk kunnen worden gebruikt.  

Een client die niet is geconfigureerd voor Internet, heeft geen beheer punten die alleen gericht zijn op internet. Workgroup-clients die zijn geconfigureerd voor Internet communiceren alleen met Internet gerichte beheer punten.  

##  <a name="the-mp-list"></a><a name="BKMK_MPList"></a> De MP-lijst  
De MP-lijst is de voorkeurs bron voor service locatie voor een client, omdat het een lijst met prioriteiten is van beheer punten die eerder door de client zijn geïdentificeerd. Deze lijst wordt door elke client gesorteerd op basis van de netwerklocatie wanneer de client de lijst bijgewerkt, en de lijst wordt vervolgens lokaal opgeslagen op de client in WMI.  

### <a name="building-the-initial-mp-list"></a>De initiële MP-lijst samen stellen  
Tijdens de installatie van de-client worden de volgende regels gebruikt voor het bouwen van de initiële MP-lijst van de client:  

- De eerste lijst bevat beheer punten die zijn opgegeven tijdens de client installatie (wanneer u de optie **SMSMP**= of **/MP** gebruikt).  
- De client vraagt AD DS naar gepubliceerde beheer punten. Het beheer punt moet afkomstig zijn van de toegewezen site van de client en moet van dezelfde product versie zijn als de client om te kunnen worden geïdentificeerd uit AD DS.  
- Als er geen beheer punt is opgegeven tijdens de client installatie en het Active Directory schema niet is uitgebreid, controleert de client DNS en WINS op gepubliceerde beheer punten.  
- Wanneer de client de eerste lijst bouwt, zijn de gegevens over sommige beheer punten in de hiërarchie mogelijk niet bekend.  

### <a name="organizing-the-mp-list"></a>De MP-lijst ordenen  
Clients ordenen hun lijst met beheer punten met behulp van de volgende classificaties:  

- **Proxy**: een beheer punt op een secundaire site.  
- **Lokaal**: elk beheer punt dat is gekoppeld aan de huidige netwerk locatie van de client, zoals gedefinieerd door de grenzen van de site. Houd rekening met de volgende informatie over grenzen:
  - Wanneer een client tot meer dan een grensgroep behoort, wordt de lijst met lokale beheerpunten bepaald door de samenvoeging van alle grenzen die de huidige netwerklocatie van de client bevatten.  
  - Lokale beheer punten zijn doorgaans een subset van de toegewezen beheer punten van een client, tenzij de client zich op een netwerk locatie bevindt die is gekoppeld aan een andere site met beheer punten die zijn grens groepen onderhoudt.   


- **Toegewezen**: elk beheer punt dat een site systeem is voor de toegewezen site van de client.  

U kunt voorkeursbeheerpunten gebruiken. Beheer punten op een site die niet zijn gekoppeld aan een grens groep of die zich niet in een grens groep bevinden die is gekoppeld aan de huidige netwerk locatie van de client, worden niet beschouwd als voorkeurs naam. Ze worden gebruikt wanneer de client geen beschikbaar voorkeurs beheer punt kan identificeren.  

### <a name="selecting-a-management-point-to-use"></a>Een te gebruiken beheerpunt selecteren  
Voor typische communicatie probeert een client een beheer punt uit de classificaties te gebruiken in de volgende volg orde, op basis van de netwerk locatie van de client:  

1.  Proxy  
2.  Lokaal  
3.  Toegewezen  

De client gebruikt het toegewezen beheerpunt echter altijd voor registratieberichten en bepaalde beleidsberichten, zelfs wanneer andere berichten worden verzonden naar een proxy of lokaal beheerpunt.  

In elke classificatie (proxy, lokaal of toegewezen) probeert de client een beheer punt te gebruiken op basis van voor keuren, in de volgende volg orde:  

1.  Met HTTPS-ondersteuning in een vertrouwd of lokaal forest (wanneer de client is geconfigureerd voor HTTPS-communicatie)  
2.  HTTPS is niet mogelijk in een vertrouwd of lokaal forest (wanneer de client is geconfigureerd voor HTTPS-communicatie)  
3.  HTTP-ondersteuning in een vertrouwd of lokaal forest  
4.  HTTP-ondersteuning in een vertrouwd of lokaal forest  

Vanuit de set beheer punten die zijn gesorteerd op voor keuren, probeert de client het eerste beheer punt in de lijst te gebruiken. Deze gesorteerde lijst met beheer punten is wille keurig en kan niet worden gerangschikt. De volg orde van de lijst kan worden gewijzigd telkens wanneer de client de MP-lijst bijwerkt.  

Wanneer een client geen contact kan maken met het eerste beheer punt, wordt elk opeenvolgend beheer punt op de lijst geprobeerd. Er wordt geprobeerd elk voorkeurs beheer punt in de classificatie te proberen voordat de niet-voorkeurs beheer punten worden uitgevoerd. Als een client niet met een beheer punt in de classificatie kan communiceren, wordt geprobeerd verbinding te maken met een voorkeurs beheer punt van de volgende classificatie, enzovoort, totdat er een beheer punt is gevonden dat moet worden gebruikt.  

Nadat een client communicatie tot stand heeft gebracht met een beheer punt, blijft het hetzelfde beheer punt gebruiken totdat:  

- 25 uur zijn verstreken.  
- De client kan niet communiceren met het beheer punt voor vijf pogingen gedurende een periode van tien minuten.

De client selecteert dan een wille keurig nieuw beheer punt dat moet worden gebruikt.  

##  <a name="active-directory"></a><a name="bkmk_ad"></a> Active Directory  
Clients die lid zijn van een domein kunnen AD DS gebruiken voor servicelocatiebepaling. Hiervoor moeten sites [gegevens publiceren naar Active Directory](../../servers/deploy/configure/publish-site-data.md).  

Een client kan AD DS gebruiken voor service locatie wanneer alle volgende voor waarden waar zijn:  

- Het Active Directory [schema is uitgebreid](../network/extend-the-active-directory-schema.md) of is uitgebreid voor System Center 2012 Configuration Manager.  
- Het [Active Directory-forest is geconfigureerd voor publicatie](../../servers/deploy/configure/publish-site-data.md)en Configuration Manager-sites zijn geconfigureerd om te publiceren.  
- De clientcomputer is lid van een Active Directory-domein en heeft toegang tot een algemene-catalogusserver.  

Als een client geen beheer punt kan vinden om te gebruiken voor service locatie vanaf AD DS, wordt geprobeerd om DNS te gebruiken.  

##  <a name="dns"></a><a name="bkmk_dns"></a> DNS  
Clients op intranet kunnen DNS gebruiken voor servicelocatiebepaling. Hiervoor moet ten minste één site in een hiërarchie informatie over beheerpunten publiceren naar DNS.  

Overweeg het gebruik van DNS voor servicelocatiebepaling als aan de volgende voorwaarden wordt voldaan:
- Het AD DS schema wordt niet uitgebreid ter ondersteuning van Configuration Manager.
- Clients op het intranet bevinden zich in een forest dat niet is ingeschakeld voor Configuration Manager publicatie.  
- U hebt clients op werkgroepcomputers en deze clients zijn niet geconfigureerd voor client beheer via internet. (Een werkgroeps-client die is geconfigureerd voor internet communiceert alleen met Internet gerichte beheer punten en maakt geen gebruik van DNS voor service locatie.)  
- U kunt [clients configureren voor het zoeken van beheerpunten via DNS](../../clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).  

Wanneer een website records voor servicelocatiebepaling van beheerpunten publiceert naar DNS:  

- Is de publicatie alleen van toepassing op beheerpunten die clientverbindingen van intranet accepteren.  
- Wordt bij de publicatie een Service Location Resource Record (SRV RR) toegevoegd aan de DNS-zone van de beheerpuntcomputer. Er moet een overeenkomende hostvermelding in DNS staan voor de computer.  

Standaard doorzoeken clients die lid zijn van een domein DNS voor beheer punt records vanuit het lokale domein van de client. U kunt een client eigenschap configureren met een domein achtervoegsel voor een domein waarvoor beheer punt informatie is gepubliceerd naar DNS.  

Zie [client computers configureren om beheer punten te vinden met DNS-publishing](../../../core/clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md)voor meer informatie over het configureren van de client eigenschap voor DNS-achtervoegsels.  

Als een client geen beheer punt kan vinden om te gebruiken voor service locatie vanuit DNS, wordt geprobeerd WINS te gebruiken.  

### <a name="publish-management-points-to-dns"></a>Beheerpunten publiceren naar DNS  
De volgende voorwaarden moeten waar zijn om beheerpunten te publiceren naar DNS:  

- Uw DNS-servers ondersteunen servicelocatiebronrecords door minstens versie 8.1.2 van BIND te gebruiken.  
- De opgegeven intranet-FQDN voor de beheer punten in Configuration Manager hebben host-items (bijvoorbeeld een record) in DNS.  

> [!IMPORTANT]  
> Configuration Manager DNS-publicatie biedt geen ondersteuning voor een niet-aaneengesloten naam ruimte. Als u een niet-aaneengesloten naam ruimte hebt, kunt u beheer punten hand matig naar DNS publiceren of een van de andere service locatie methoden gebruiken die in deze sectie worden beschreven.  

**Als uw DNS-servers automatische updates ondersteunen**, kunt u Configuration Manager zodanig configureren dat beheer punten op het intranet automatisch naar DNS worden gepubliceerd, of u kunt deze records hand matig publiceren naar DNS. Als beheerpunten naar DNS worden gepubliceerd, worden hun intranet-FQDN en poortnummer gepubliceerd in het servicelocatierecord (SRV-record). U configureert DNS-publicatie op een site in de eigenschappen van de beheer punt component van de site. Zie  [site onderdelen voor Configuration Manager](../../../core/servers/deploy/configure/site-components.md)voor meer informatie.  

**Als uw DNS-zone is ingesteld op ' alleen beveiligd ' voor dynamische updates**, kan alleen het eerste beheer punt dat naar DNS wordt gepubliceerd, worden uitgevoerd met de standaard machtigingen.

Als slechts één beheer punt de DNS-record kan publiceren en wijzigen en de beheer punt server in orde is, kunnen clients de volledige MP-lijst van dat beheer punt ophalen en vervolgens het voorkeurs beheer punt vinden.


**U kunt beheerpunten handmatig naar DNS publiceren als uw DNS-servers geen automatische updates**, maar wel servicelocatierecords ondersteunen. Hiervoor moet u handmatig het servicelocatiebronrecord (SRV RR) in DNS opgeven.  

Configuration Manager ondersteunt RFC 2782 voor service locatie records. Deze records hebben de volgende indeling:   *_Service. _Proto. naam TTL class SRV-prioriteits gewicht poort doel*  

Geef de volgende waarden op om een beheer punt te publiceren naar Configuration Manager:  

- **_Service**: Voer **_mssms_mp**_ &lt; \> site code in, waarbij &lt; \> naam van de locatie van het beheer punt is.  
- **._Proto**: geef **._tcp**op.  
- **.Naam**: voer het DNS-achtervoegsel in van het beheerpunt, bijvoorbeeld **contoso.com**.  
- **TTL**: voer **14400**in, wat gelijk staat aan vier uur.  
- **Klasse**: geef **IN** op (in overeenstemming met RFC 1035).  
- **Priority**: Configuration Manager gebruikt dit veld niet.
- **Gewicht**: Configuration Manager gebruikt dit veld niet.  
- **Poort**: voer het poortnummer in dat door het beheerpunt wordt gebruikt. Bijvoorbeeld **80** voor HTTP en **443** voor HTTPS.  

  > [!NOTE]  
  >  De SRV-record poort moet overeenkomen met de communicatie poort die door het beheer punt wordt gebruikt. Standaard is dit **80** voor http-communicatie en **443** voor HTTPS-communicatie.  

- **Doel**: Voer de intranet-FQDN in dat is opgegeven voor het sitesysteem dat is geconfigureerd met de siterol van het beheerpunt.  

Als u Windows Server DNS gebruikt, kunt u de volgende procedure gebruiken om dit DNS-record in te voeren voor intranet-beheerpunten. Als u een verschillende implementatie voor DNS gebruikt, dient u de informatie in deze sectie over de veldwaarden te gebruiken en de DNS-documentatie te raadplegen om deze procedure aan te passen.  

##### <a name="to-configure-automatic-publishing"></a>Automatische publicatie configureren:  

1.  Vouw in de Configuration Manager-console **beheer**  >  **site configuratie**  >  **sites**uit.  

2.  Selecteer uw site en kies vervolgens **site onderdelen configureren**.  

3.  Kies **beheer punt**.  

4.  Selecteer de beheer punten die u wilt publiceren. (Deze selectie geldt voor publicatie naar AD DS en DNS.)  

5.  Schakel het selectie vakje in om te publiceren naar DNS. Dit vak:  

    - Hiermee kunt u selecteren welke beheer punten u wilt publiceren naar DNS.  

    - Hiermee wordt publiceren naar AD DS niet geconfigureerd.  

##### <a name="to-manually-publish-management-points-to-dns-on-windows-server"></a>Handmatig beheerpunten publiceren naar DNS op Windows Server  

1.  Geef in de Configuration Manager-console de intranet-FQDN op van site systemen.  

2.  Selecteer de DNS-zone voor de beheerpuntcomputer in de DNS-beheerconsole.  

3.  Verifieer of er een hostrecord is (A of AAAA) voor de intranet-FQDN van het sitesysteem. Maak dit record als het niet bestaat.  

4.  Met de optie **nieuwe andere records** kiest u **service locatie (SRV)** in het dialoog **venster bron record type** , kiest u **record maken**, voert u de volgende informatie in en kiest u **gereed**:  

    - **Domein**: voer indien nodig het DNS-achtervoegsel in van het beheerpunt, bijvoorbeeld **contoso.com**.  
    - **Service**: Typ **_mssms_mp**_ &lt; \> code site, &lt; waarbij \> site-naam van het beheer punt is.  
    - **Protocol**: typ **_tcp**.  
    - **Priority**: Configuration Manager gebruikt dit veld niet.  
    - **Gewicht**: Configuration Manager gebruikt dit veld niet.  
    - **Poort**: voer het poortnummer in dat door het beheerpunt wordt gebruikt. Bijvoorbeeld **80** voor HTTP en **443** voor HTTPS.  

      > [!NOTE]  
      > De SRV-record poort moet overeenkomen met de communicatie poort die door het beheer punt wordt gebruikt. Standaard is dit **80** voor http-communicatie en **443** voor HTTPS-communicatie.  

    - **Host die deze service aanbiedt**: Voer de intranet-FQDN in die is opgegeven voor het site systeem dat is geconfigureerd met de siterol van het beheer punt.  

Herhaal deze stappen voor elk beheerpunt op het intranet dat u wilt publiceren naar DNS.  

##  <a name="wins"></a><a name="bkmk_wins"></a> WINS  
Als andere servicelocatiemechanismen mislukken, kunnen clients een initieel beheerpunt vinden door WINS te controleren.  

Standaard publiceert een primaire site het eerste beheer punt op de site die is geconfigureerd voor HTTP en het eerste beheer punt dat is geconfigureerd voor HTTPS.  

Als u niet wilt dat clients een HTTP-beheerpunt in WINS vinden, kunt u clients configureren met de Client.msi-eigenschap **SMSDIRECTORYLOOKUP=NOWINS**van CCMSetup.exe.