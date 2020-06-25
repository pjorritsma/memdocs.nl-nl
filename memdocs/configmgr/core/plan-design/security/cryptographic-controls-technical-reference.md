---
title: Technische naslaginformatie voor cryptografische besturingselementen
titleSuffix: Configuration Manager
description: Meer informatie over hoe u met behulp van ondertekening en versleuteling aanvallen kunt beveiligen tegen het lezen van gegevens in Configuration Manager.
ms.date: 12/08/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe50aad3cb35ab5908f604560f4dcd22800919a5
ms.sourcegitcommit: 22e1095a41213372c52d85c58b18cbabaf2300ac
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/25/2020
ms.locfileid: "85353442"
---
# <a name="cryptographic-controls-technical-reference"></a>Technische naslaginformatie voor cryptografische besturingselementen

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager gebruikt ondertekening en versleuteling om het beheer van de apparaten in de Configuration Manager hiërarchie te beveiligen. Als er bij het ondertekenen gegevens zijn gewijzigd tijdens de overdracht, wordt deze verwijderd. Versleuteling helpt te voor komen dat een aanvaller de gegevens kan lezen door gebruik te maken van een netwerkprotocol analyse.  

 Het primaire hash-algoritme dat Configuration Manager gebruikt voor ondertekening is SHA-256. Wanneer twee Configuration Manager-sites met elkaar communiceren, ondertekenen ze hun communicatie met SHA-256. Het primaire versleutelings algoritme dat in Configuration Manager is geïmplementeerd, is 3DES. Dit wordt gebruikt voor het opslaan van gegevens in de Configuration Manager-Data Base en voor client-HTTP-communicatie. Wanneer u client communicatie via HTTPS gebruikt, kunt u uw open bare-sleutel infrastructuur (PKI) configureren voor het gebruik van RSA-certificaten met de maximale hash-algoritmen en sleutel lengten die zijn gedocumenteerd in [vereisten voor PKI-certificaten](../network/pki-certificate-requirements.md).  

 Voor de meeste cryptografische bewerkingen voor op Windows gebaseerde besturings systemen maakt Configuration Manager gebruik van SHA-2, 3DES en AES en RSA-algoritmen van de Windows CryptoAPI-bibliotheek rsaenh.dll.  

> [!IMPORTANT]  
>  Zie [About SSL Vulnerabilities](#about-ssl-vulnerabilities)voor informatie over de aanbevolen wijzigingen in reactie op SSL-beveiligingslekken in.  

##  <a name="cryptographic-controls-for-configuration-manager-operations"></a>Cryptografische besturings elementen voor Configuration Manager bewerkingen  
 Informatie in Configuration Manager kan worden ondertekend en versleuteld, ongeacht of u PKI-certificaten gebruikt met Configuration Manager.  

### <a name="policy-signing-and-encryption"></a>Ondertekening en versleuteling van beleid  
 Toewijzingen van clientbeleid worden ondertekend door het zelfondertekende handtekeningcertificaat van de siteserver om het risico te helpen voorkomen op een aangetast verzendbeleid van een beheerpunt waarmee is geknoeid. Dit is belang rijk als u gebruikmaakt van client beheer op internet, omdat deze omgeving een beheer punt vereist dat wordt blootgesteld aan Internet communicatie.  

 Beleid wordt versleuteld met 3DES als het gevoelige gegevens bevat. Beleid dat gevoelige gegevens bevat, wordt alleen verzonden naar geautoriseerde clients. Beleid dat geen gevoelige gegevens bevat, wordt niet versleuteld.  

 Wanneer beleid op de clients wordt opgeslagen, wordt het versleuteld met behulp van DPAPI (Data Protection Application Programming Interface).  

### <a name="policy-hashing"></a>Hashing van beleid  
 Wanneer Configuration Manager clients beleid aanvragen, wordt eerst een beleids toewijzing opgehaald, zodat ze weten welk beleid van toepassing is en vervolgens alleen die beleids teksten worden gevraagd. Elke beleidtoewijzing bevat de berekende hash voor de overeenkomstige beleidhoofdtekst. De client haalt de van toepassing zijnde beleidhoofdteksten op en berekent vervolgens de hash op die hoofdtekst. Als de hash op de gedownloade beleidhoofdtekst niet overeenkomt met de hash in de beleidtoewijzing, verwijdert de client de beleidhoofdtekst.  

 Het hash-algoritme voor beleid is SHA-1 en SHA-256.  

### <a name="content-hashing"></a>Hashing van inhoud  

De distributiebeheerservice op de siteserver hasht de inhoudsbestanden voor alle pakketten. De beleidsprovider neemt de hash op in het softwaredistributiebeleid. Wanneer de Configuration Manager-client de inhoud downloadt, genereert de client de hash lokaal opnieuw en vergelijkt deze met die in het beleid. Als de hashes overeenkomen, werd de inhoud niet gewijzigd en zal de client het installeren. Zodra er één enkele byte is gewijzigd, komen de hashes niet overeen en zal de software niet worden geïnstalleerd. Deze controle helpt om te garanderen dat de correcte software wordt geïnstalleerd, omdat de werkelijke inhoud aan het beleid wordt getoetst.  

Het standaard hash-algoritme voor inhoud is SHA-256.

Niet alle apparaten kunnen inhoud-hashing ondersteunen. De uitzonde ringen zijn onder andere:  

- Windows-clients wanneer ze App-V-inhoud streamen.  

- Windows Phone-clients, hoewel deze clients de hand tekening verifiëren van een toepassing die is ondertekend door een vertrouwde bron.  

- Windows RT-client, hoewel deze clients de hand tekening verifiëren van een toepassing die is ondertekend door een vertrouwde bron en ook validatie van de volledige pakket naam (PFN) gebruiken.  

- Clients met Linux- of UNIX-versies die SHA-256 niet ondersteunen. Zie [planning voor client implementatie op Linux-en UNIX-computers](../../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md)voor meer informatie.  

### <a name="inventory-signing-and-encryption"></a>Inventaris hand tekening en versleuteling  
 Inventaris die clients verzenden naar beheerpunten wordt altijd ondertekend door apparaten, ongeacht of ze communiceren met beheerpunten via HTTP of HTTPS. Als ze HTTP gebruiken, kunt u kiezen om deze gegevens te versleutelen, wat een aanbevolen beveiligingsprocedure is.  

### <a name="state-migration-encryption"></a>Status migratie versleuteling  
 Gegevens die zijn opgeslagen op statusmigratiepunten voor besturingssysteemimplementatie wordt altijd versleuteld door het hulpprogramma voor migratie van gebruikersstatus (USMT) door 3DES te gebruiken.  

### <a name="encryption-for-multicast-packages-to-deploy-operating-systems"></a>Versleuteling voor multi cast-pakketten om besturings systemen te implementeren  
 Voor elk pakket voor besturingssysteemimplementatie kunt u versleuteling inschakelen wanneer het pakket wordt verzonden naar computers door gebruik te maken van multicast. De versleuteling gebruikt Advanced Encryption Standard (AES). Als u versleuteling inschakelt, is er geen aanvullende certificaatconfiguratie vereist. Het multicast-distributiepunt genereert automatisch symmetrische sleutels voor het versleutelen van het pakket. Elk pakket heeft een andere versleutelingssleutel. De sleutel wordt opgeslagen op het multicast-distributiepunt met standaard Windows-API's. Wanneer de client verbinding maakt met de multicast-sessie, gebeurt de uitwisseling van de sleutel over een kanaal dat is versleuteld met het door PKI uitgegeven certificaat voor clientverificatie (als de client HTTPS gebruikt) of met het zelfondertekende certificaat (als de client HTTP gebruikt). De client slaat de sleutel alleen op in het geheugen voor de duur van de multicast-sessie.  

### <a name="encryption-for-media-to-deploy-operating-systems"></a>Versleuteling voor media om besturings systemen te implementeren  
 Wanneer u media gebruikt om besturings systemen te implementeren en een wacht woord opgeeft om de media te beveiligen, worden de omgevings variabelen versleuteld met behulp van Advanced Encryption Standard (AES) met een 128-bits sleutel grootte. Andere gegevens op de media, waaronder pakketten en inhoud voor toepassingen, worden niet versleuteld.  

### <a name="encryption-for-content-that-is-hosted-on-cloud-based-distribution-points"></a>Versleuteling voor inhoud die wordt gehost op cloud-gebaseerde distributie punten  
 Vanaf System Center 2012 Configuration Manager SP1, wanneer u Cloud distributiepunten gebruikt, wordt de inhoud die u uploadt naar deze distributie punten versleuteld met behulp van Advanced Encryption Standard (AES) met een 256-bits sleutel grootte. De inhoud wordt opnieuw versleuteld wanneer u die bijwerkt. Als clients de inhoud downloaden, wordt deze versleuteld en beveiligd door de HTTPS-verbinding.  

### <a name="signing-in-software-updates"></a>Software-updates aanmelden  
 Alle software-updates moeten worden aangemeld door een vertrouwde uitgever om te beveiligen tegen knoeien. Op clientcomputers scant de Windows Update Agent (WUA) naar de updates uit de catalogus, maar de update zal niet worden geïnstalleerd als het digitale certificaat niet kan worden gevonden in het archief Vertrouwde uitgevers op de lokale computer. Als er een zelfondertekend certificaat werd gebruikt voor het publiceren van de updatecatalogus, zoals WSUS Publishers Self-signed, moet het certificaat ook in het certificaatarchief van de Vertrouwde basiscertificeringsinstanties op de lokale computer aanwezig zijn om de geldigheid van het certificaat te verifiëren. WUA controleert ook of de instelling **Ondertekende inhoud van groepsbeleid van Microsoft-updateservicelocatie via intranet toestaan** is ingeschakeld op de lokale computer. Deze beleidsinstelling moet worden ingeschakeld voor WUA om te scannen naar de updates die zijn gemaakt en gepubliceerd met Updates Publisher.  

 Als software-updates in System Center Updates Publisher zijn gepubliceerd, ondertekent een digitaal certificaat de software-updates wanneer ze naar een updateserver zijn gepubliceerd. U kunt een PKI-certificaat opgeven of de Updates Publisher configureren om een zelfondertekend certificaat te genereren om de software-update te ondertekenen.  

### <a name="signed-configuration-data-for-compliance-settings"></a>Ondertekende configuratie gegevens voor compatibiliteits instellingen  
 Wanneer u configuratie gegevens importeert, controleert Configuration Manager de digitale hand tekening van het bestand. Als de bestanden niet zijn ondertekend of als de verificatiecontrole van de digitale handtekening mislukt, ontvangt u een waarschuwing en wordt u gevraagd of u wilt doorgaan met importeren. Blijf de configuratiegegevens alleen importeren als u de uitgever en de integriteit van de bestanden expliciet vertrouwt.  

### <a name="encryption-and-hashing-for-client-notification"></a>Versleuteling en hashing voor client meldingen  
 Als u gebruik maakt van clientmeldingen, zal alle communicatie TLS en de meeste geavanceerde versleuteling gebruiken die de server en de clientbesturingssystemen kunnen onderhandelen. Een client computer met Windows 7 en een beheer punt waarop Windows Server 2008 R2 wordt uitgevoerd, kan bijvoorbeeld ondersteuning bieden voor 128-bits AES-versleuteling, terwijl een client computer waarop Vista wordt uitgevoerd naar hetzelfde beheer punt, wordt onderhandeld naar 3DES-versleuteling. Dezelfde onderhandeling doet zich voor bij hashing voor pakketten die worden overgedragen tijdens clientmeldingen, waarvoor SHA-1 of SHA-2 wordt gebruikt.  

##  <a name="certificates-used-by-configuration-manager"></a>Certificaten die worden gebruikt door Configuration Manager  
 Zie [PKI-certificaat vereisten](../network/pki-certificate-requirements.md)voor een lijst met PKI-certificaten (Public Key Infrastructure) die kunnen worden gebruikt door Configuration Manager, speciale vereisten of beperkingen en hoe de certificaten worden gebruikt. Deze lijst bevat de ondersteunde hash-algoritmen en sleutellengten. De meeste certificaten ondersteunen sleutellengten van SHA-256 en 2048 bits.  

> [!NOTE]  
>  Alle certificaten die Configuration Manager gebruikt, mogen alleen enkel-byte-tekens bevatten in de onderwerpnaam of alternatieve naam voor het onderwerp.  

 PKI-certificaten zijn vereist voor de volgende scenario's:  

- Wanneer u Configuration Manager-clients op internet beheert.  

- Wanneer u Configuration Manager-clients op mobiele apparaten beheert.  

- Als u Mac-computers beheert.  

- Als u cloud-gebaseerde distributiepunten gebruikt.  

  Voor de meeste andere Configuration Manager communicaties die certificaten vereisen voor verificatie, ondertekening of versleuteling, gebruikt Configuration Manager automatisch PKI-certificaten als ze beschikbaar zijn. Als deze niet beschikbaar zijn, genereert Configuration Manager zelfondertekende certificaten.  

  Configuration Manager gebruikt geen PKI-certificaten wanneer het mobiele apparaten beheert met behulp van de Exchange Server-connector.  

### <a name="mobile-device-management-and-pki-certificates"></a>Beheer van mobiele apparaten en PKI-certificaten  
 Als het mobiele apparaat niet is vergrendeld door de mobiele operator, kunt u Configuration Manager of Microsoft Intune gebruiken om een client certificaat aan te vragen en te installeren. Dit certificaat biedt wederzijdse verificatie tussen de client op het mobiele apparaat en Configuration Manager site systemen of Microsoft Intune Services. Als uw mobiele apparaat is vergrendeld, kunt u Configuration Manager of intune niet gebruiken om certificaten te implementeren.  

 Als u hardware-inventaris voor mobiele apparaten inschakelt, worden de certificaten die op het mobiele apparaat zijn geïnstalleerd, ook door Configuration Manager of intune geinventariseerd.   

### <a name="operating-system-deployment-and-pki-certificates"></a>Implementatie van het besturings systeem en PKI-certificaten  
 Wanneer u Configuration Manager gebruikt om besturings systemen te implementeren en een beheer punt HTTPS-client verbindingen vereist, moet de client computer ook een certificaat hebben om te communiceren met het beheer punt, zelfs als het zich in een overgangs fase bevindt, zoals opstarten vanaf een taken reeks media of een distributie punt met PXE-functionaliteit. Als u dit scenario wilt ondersteunen, moet u een PKI-certificaat voor client verificatie maken en dit exporteren met de persoonlijke sleutel, en het vervolgens importeren naar de site server eigenschappen en ook het vertrouwde basis-CA-certificaat van het beheer punt toevoegen.  

 Als u opstartbare media maakt, importeert u het certificaat voor clientverificatie wanneer u de opstartbare media maakt. Configureer een wachtwoord op de opstartbare media om te helpen de persoonlijke sleutel en andere gevoelige gegevens te beschermen die in de takenreeks zijn geconfigureerd. Elke computer die opstart vanaf de opstartbare media, zal hetzelfde certificaat tonen aan het beheerpunt zoals vereist voor clientfuncties zoals het aanvragen van het clientbeleid.  

 Als u een PXE-opstartapparaat gebruikt, importeert u het certificaat voor clientverificatie naar het distributiepunt met PXE-functionaliteit en het gebruikt hetzelfde certificaat voor elke client die opstart vanuit dat distributiepunt met PXE-functionaliteit. Uit veiligheidsoverwegingen wordt het aanbevolen dat gebruikers die hun computers aansluiten op een PXE-service een wachtwoord moeten ingeven om te helpen de persoonlijke sleutel en andere gevoelige gegevens in de takenreeksen te beschermen.  

 Blokkeer de certificaten voor clientverificatie, als ermee is geknoeid, in het knooppunt **Certificaten** in de werkruimte **Beheer,** knooppunt **Beveiliging** . Om deze certificaten te beheren, moet u het recht **Implementatiecertificaat van het besturingssysteem beheren** .  

 Nadat het besturings systeem is geïmplementeerd en de Configuration Manager is geïnstalleerd, heeft de client een eigen PKI-certificaat voor client verificatie nodig voor HTTPS-client communicatie.  

### <a name="isv-proxy-solutions-and-pki-certificates"></a>ISV-proxy oplossingen en PKI-certificaten  
 Independent Software Vendors (Isv's) kunnen toepassingen maken waarmee Configuration Manager worden uitgebreid. Een ISV zou bijvoorbeeld extensies kunnen maken om niet-Windows clientplatforms zoals Macintosh of UNIX-computers te ondersteunen. Als de sitesystemen echter HTTPS-clientverbindingen vereisen, moeten de clients ook PKI-certificaten gebruiken voor communicatie met de site. Configuration Manager biedt de mogelijkheid om een certificaat toe te wijzen aan de ISV-proxy die communicatie mogelijk maakt tussen de ISV-Proxy-clients en het beheer punt. Als u extensies gebruikt die ISV-proxycertificaten vereisen, raadpleeg dan de documentatie voor dat product. Zie de Configuration Manager Software Developer Kit (SDK) voor meer informatie over het maken van ISV-proxy certificaten.  

 Blokkeer het ISV-certificaat, als ermee is geknoeid, in het knooppunt **Certificaten** van de werkruimte **Beheer** in het knooppunt **Beveiliging** .  

### <a name="asset-intelligence-and-certificates"></a>Asset Intelligence en certificaten  
 Configuration Manager wordt geïnstalleerd met een X. 509-certificaat dat door het Asset Intelligence synchronisatie punt wordt gebruikt om verbinding te maken met micro soft. Configuration Manager gebruikt dit certificaat om een certificaat voor client verificatie aan te vragen bij de micro soft-certificaat service. Het certificaat voor clientverificatie wordt geïnstalleerd op de sitesysteemserver van het Asset Intelligence-synchronisatiepunt en het wordt gebruikt om de server met Microsoft te verifiëren. Configuration Manager gebruikt het certificaat voor clientverificatie om de Asset Intelligence-catalogus te downloaden en softwaretitels te uploaden.  

 Dit certificaat heeft een sleutellengte van 1024 bits.  

### <a name="cloud-based-distribution-points-and-certificates"></a>Cloud-gebaseerde distributie punten en certificaten  
 Vanaf System Center 2012 Configuration Manager SP1 is voor distributie punten in de Cloud een beheer certificaat (zelf ondertekend of PKI) vereist dat u naar Microsoft Azure uploadt. Dit beheercertificaat vereist een functionaliteit voor serververificatie en een sleutellengte van het certificaat van 2048 bits. Daarnaast moet u een servicecertificaat configureren voor elk distributiepunt in de cloud, dat niet zelfondertekend kan zijn, maar ook de functionaliteit voor serververificatie en een minimum sleutellengte van het certificaat van 2048 bits heeft.  

> [!NOTE]  
>  Het zelfondertekende beheercertificaat dient uitsluitend voor tests en niet voor gebruik op productienetwerken.  

 Clients vereisen geen PKI-certificaat van de client om distributiepunten in de cloud te gebruiken; ze verifiëren naar het beheer met behulp van hetzij een zelfondertekend certificaat hetzij een PKI-certificaat van de client. Het beheer punt geeft vervolgens een Configuration Manager toegangs token aan de client door, die de client aan het cloud-gebaseerde distributie punt presenteert. Het token is 8 uur lang geldig.  

### <a name="the-microsoft-intune-connector-and-certificates"></a>De Microsoft Intune-connector en certificaten  
 Wanneer Microsoft Intune mobiele apparaten registreert, kunt u deze mobiele apparaten beheren in Configuration Manager door een Microsoft Intune-connector te maken. De connector gebruikt een PKI-certificaat met de mogelijkheid voor client verificatie om Configuration Manager te verifiëren voor Microsoft Intune en om alle informatie ertussen over te dragen met behulp van SSL. De sleutelgrootte van het certificaat is 2048 bits en gebruikt het hash-algoritme SHA-1.  

 Wanneer u de connector installeert, wordt een handtekeningcertificaat gemaakt en opgeslagen op de siteserver voor het extern laden van sleutels, en wordt er een versleutelingscertificaat gemaakt en opgeslagen op het certificaatregistratiepunt om de Simple Certificate Enrollment Protocol (SCEP)-vraag te versleutelen. Deze certificaten hebben ook een sleutelgrootte van 2048 bits en gebruiken het hash-algoritme SHA-1.  

 Wanneer intune mobiele apparaten registreert, wordt er een PKI-certificaat op het mobiele apparaat geïnstalleerd. Dit certificaat heeft ook een mogelijkheid voor clientverificatie, gebruikt een sleutelgrootte van 2048 bits en gebruikt het hash-algoritme SHA-1.  

 Deze PKI-certificaten worden automatisch aangevraagd, gegenereerd en geïnstalleerd door Microsoft Intune.  

### <a name="crl-checking-for-pki-certificates"></a>CRL-controle voor PKI-certificaten  
 Een PKI-certificaatintrekkingslijst (CRL) verhoogt de administratieve en verwerkingsoverhead, maar het is veiliger. Als CRL-controle echter is ingeschakeld, maar de CRL niet beschikbaar is, mislukt de PKI-verbinding. Zie [beveiliging en privacy voor Configuration Manager](security-and-privacy.md)voor meer informatie.  

 Controle van de certificaatintrekkingslijst (CRL) is standaard ingeschakeld in IIS, dus als u een CRL met uw PKI-implementatie gebruikt, is er niets meer om te configureren op de meeste Configuration Manager-site systemen die IIS uitvoeren. Een uitzondering hierop zijn de software-updates, die een handmatige stap vereisen om CRL-controle in te schakelen om de handtekeningen op software-updatebestanden te controleren.  

 CRL-controle wordt standaard ingeschakeld voor clientcomputers wanneer ze HTTPS-clientverbindingen gebruiken. U kunt CRL-controle niet uitschakelen voor clients op Mac-computers in Configuration Manager SP1 of hoger.  

 CRL-controle wordt niet ondersteund voor de volgende verbindingen in Configuration Manager:  

-   Server-naar-server-verbindingen.  

-   Mobiele apparaten die zijn Inge schreven door Configuration Manager.  

-   Mobiele apparaten die zijn Inge schreven door Microsoft Intune.  

##  <a name="cryptographic-controls-for-server-communication"></a>Cryptografische besturings elementen voor Server communicatie  
 Configuration Manager gebruikt de volgende cryptografische besturings elementen voor Server communicatie.  

### <a name="server-communication-within-a-site"></a>Server communicatie binnen een site  
 Elke site systeem server gebruikt een certificaat om gegevens over te brengen naar andere site systemen in dezelfde Configuration Manager-site. Sommige sitesysteemrollen gebruiken ook certificaten voor verificatie. Als u het inschrijvingsproxypunt bijvoorbeeld op een server installeert en het inschrijvingspunt op een andere server, kunnen ze elkaar verifiëren met behulp van dit identiteitscertificaat. Als Configuration Manager een certificaat voor deze communicatie gebruikt, wordt dit door Configuration Manager automatisch gebruikt als er een PKI-certificaat beschikbaar is dat de mogelijkheid voor Server verificatie heeft. Als dat niet het geval is, wordt door Configuration Manager een zelfondertekend certificaat gegenereerd. Dit zelfondertekende certificaat heeft een mogelijkheid voor serververificatie, gebruikt SHA-256 en heeft een sleutellengte van 2048 bits. Configuration Manager kopieert het certificaat naar het archief Vertrouwde personen op andere site systeem servers die het site systeem mogelijk moeten vertrouwen. Sitesystemen kunnen elkaar dan vertrouwen met behulp van deze certificaten en PeerTrust.  

 Naast dit certificaat voor elke site systeem server, Configuration Manager genereert een zelfondertekend certificaat voor de meeste site systeem rollen. Wanneer er meer dan één exemplaar van de sitesysteemrol in dezelfde site is, delen ze hetzelfde certificaat. U kunt bijvoorbeeld meerdere beheerpunten of meerdere inschrijvingspunten in dezelfde site hebben. Dit zelfondertekende certificaat gebruikt ook SHA-256 en heeft een sleutellengte van 2048 bits. Het wordt ook gekopieerd naar het archief Vertrouwde personen op sitesysteemservers die het mogelijk moeten  vertrouwen. De volgende sitesysteemrollen genereren dit certificaat:  

- Application Catalog-webservicepunt  

- Application Catalog-websitepunt  

- Asset Intelligence-synchronisatiepunt  

- Certificaatregistratiepunt  

- Endpoint Protection-punt  

- Inschrijvingspunt  

- Terugvalstatuspunt  

- Beheerpunt  

- Multicast-distributiepunt  

- Reporting Services-punt  

- Software-updatepunt  

- Statusmigratiepunt  

- Microsoft Intune-connector  

Deze certificaten worden automatisch beheerd door Configuration Manager, en, indien nodig, automatisch gegenereerd.  

Configuration Manager gebruikt ook een certificaat voor client verificatie om status berichten van het distributie punt naar het beheer punt te verzenden. Wanneer het beheerpunt enkel is geconfigureerd voor HTTPS-clientverbindingen, moet u een PKI-certificaat gebruiken. Als het beheerpunt HTTP-verbindingen aanvaardt, kunt u een PKI-certificaat gebruiken of de optie selecteren om een zelfondertekend certificaat te gebruiken dat de mogelijkheid voor clientverificatie heeft, SHA-256 gebruikt en een sleutellengte van 2048 bits heeft.  

### <a name="server-communication-between-sites"></a>Server communicatie tussen sites  
 Configuration Manager verzendt gegevens tussen sites met behulp van database replicatie en replicatie op basis van een bestand. Zie [communicatie tussen eind punten](../hierarchy/communications-between-endpoints.md)voor meer informatie.  

 Configuration Manager configureert automatisch de database replicatie tussen sites en gebruikt PKI-certificaten die de mogelijkheid voor Server verificatie hebben als deze beschikbaar zijn. Als dat niet het geval is, Configuration Manager zelfondertekende certificaten voor Server verificatie maken. In beide gevallen wordt verificatie tussen sites tot stand gebracht met behulp van certificaten in het archief Vertrouwde Personen dat PeerTrust gebruikt. Dit certificaat archief wordt gebruikt om ervoor te zorgen dat alleen de SQL Server computers die door de Configuration Manager-hiërarchie worden gebruikt, deel nemen aan de replicatie van site-naar-site. Terwijl primaire sites en de centrale beheersite configuratiewijzigingen kunnen repliceren naar alle sites in de hiërarchie, kunnen secundaire sites configuratiewijzigingen enkel repliceren naar de bovenliggende site ervan.  

 Siteservers brengen communicatie van site naar site tot stand met behulp van de beveiligde sleuteluitwisseling die automatisch plaatsvindt. De verzendende siteserver genereert een hash en tekent het met zijn persoonlijke sleutel. De ontvangende siteserver controleert de handtekening met behulp van de publieke sleutel en vergelijkt de hash met een lokaal gegenereerde waarde. Als ze overeenkomen, worden de gerepliceerde gegevens in de ontvangende site aanvaard. Als de waarden niet overeenkomen, Configuration Manager weigert de replicatie gegevens.  

 Database replicatie in Configuration Manager gebruikt de SQL Server Service Broker om gegevens over te dragen tussen sites met behulp van de volgende mechanismen:  

- Verbinding van SQL Server naar SQL Server: dit maakt gebruik van Windows-referenties voor serververificatie en zelfondertekende certificaten met 1024 bits om de gegevens te ondertekenen en versleutelen met behulp van Advanced Encryption Standard (AES). Als er PKI-certificaten met de functionaliteit voor serververificatie beschikbaar zijn, zullen deze worden gebruikt. Het certificaat moet zich in het persoonlijke archief voor het certificaatarchief van de computer bevinden.  

- SQL Service Broker: dit maakt gebruik van zelfondertekende certificaten met 2048 bits voor verificatie en om de gegevens te ondertekenen en versleutelen met behulp van Advanced Encryption Standard (AES). Het certificaat moet zich in de hoofddatabase van de SQL Server bevinden.  

  Replicatie op basis van een bestand gebruikt het SMB-protocol (Server Message Block) en gebruikt SHA-256 om de gegevens te ondertekenen die niet zijn versleuteld, maar geen gevoelige gegevens bevatten. Als u deze gegevens wilt versleutelen, kunt u IPsec gebruiken en moet u dit onafhankelijk van Configuration Manager implementeren.  

##  <a name="cryptographic-controls-for-clients-that-use-https-communication-to-site-systems"></a>Cryptografische besturings elementen voor clients die HTTPS-communicatie naar site systemen gebruiken  
 Wanneer sitesysteemrollen clientverbindingen aanvaarden, kunt u ze configureren om HTTPS- en HTTP-verbindingen, of enkel HTTPS-verbindingen te aanvaarden. Sitesysteemrollen die verbindingen van het internet aanvaarden, aanvaarden enkel clientverbindingen over HTTPS.  

 Clientverbindingen over HTTPS bieden een hogere veiligheidsgraad door integratie met een PKI (Public Key Infrastructure) om communicatie van de client naar de server te helpen beschermen. HTTPS-clientverbindingen configureren zonder een grondig begrip van PKI-planning, implementatie en bewerkingen kan u echter nog in een kwetsbare positie plaatsen. Als u uw basiscertificeringsinstantie bijvoorbeeld niet beveiligt, kunnen aanvallers knoeien met het vertrouwen van uw volledige PKI-infrastructuur. Als u er niet in slaagt de PKI-certificaten te implementeren en beheren met behulp van gecontroleerde en beveiligde processen, kan dit leiden tot onbeheerde clients die geen kritische software-updates of pakketten kunnen ontvangen.  

> [!IMPORTANT]  
>  De PKI-certificaten die worden gebruikt voor clientcommunicatie beschermen enkel de communicatie tussen de client en sommige sitesystemen. Ze beschermen niet het communicatiekanaal tussen de siteserver en sitesystemen of tussen siteservers.  

### <a name="communication-that-is-unencrypted-when-clients-use-https-communication"></a>Communicatie die niet versleuteld is wanneer clients HTTPS-communicatie gebruiken  
 Wanneer clients communiceren met sitesystemen met behulp van HTTPS, worden communicaties gewoonlijk versleuteld over SSL. In de volgende situaties communiceren clients echter met sitesystemen zonder het gebruik van versleuteling:  

- Clients slagen er niet in een HTTPS-verbinding tot stand te brengen op het intranet en vallen terug op het gebruik van HTTP wanneer sitesystemen deze configuratie toestaan.  

- Communicatie met de volgende sitesysteemrollen:  

  -   Client stuurt statusberichten naar het terugvalstatuspunt  

  -   Client stuurt PXE-aanvragen naar een distributiepunt met PXE-functionaliteit  

  -   Client stuurt meldinggegevens naar een beheerpunt  

  Reporting services-punten zijn geconfigureerd om HTTP of HTTPS te gebruiken onafhankelijk van de communicatiemodus van de client.  

##  <a name="cryptographic-controls-for-clients-chat-use-http-communication-to-site-systems"></a>Cryptografische besturings elementen voor clients chatten HTTP-communicatie met site systemen gebruiken  
 Wanneer clients HTTP-communicatie naar site systeem rollen gebruiken, kunnen ze PKI-certificaten gebruiken voor client verificatie of zelfondertekende certificaten die Configuration Manager gegenereerd. Wanneer Configuration Manager zelfondertekende certificaten genereert, hebben ze een aangepaste object-id voor ondertekening en versleuteling, en worden deze certificaten gebruikt om de client op unieke wijze te identificeren. Voor alle ondersteunde besturingssystemen behalve Windows Server 2003 gebruiken deze zelfondertekende certificaten SHA-256 en hebben ze een sleutellengte van 2048 bits. Voor Windows Server 2003 wordt SHA1 gebruikt met een sleutellengte van 1024 bits.  

### <a name="operating-system-deployment-and-self-signed-certificates"></a>Implementatie van het besturings systeem en zelfondertekende certificaten  
 Wanneer u Configuration Manager gebruikt om besturings systemen te implementeren met zelfondertekende certificaten, moet een client computer ook een certificaat hebben om te communiceren met het beheer punt, zelfs als de computer zich in een overgangs fase bevindt, zoals opstarten vanaf een taken reeks media of een distributie punt met PXE-functionaliteit. Om dit scenario te ondersteunen voor HTTP-client verbindingen, genereert Configuration Manager zelfondertekende certificaten met een aangepaste object-id voor ondertekening en versleuteling, en worden deze certificaten gebruikt om de client op unieke wijze te identificeren. Voor alle ondersteunde besturingssystemen behalve Windows Server 2003 gebruiken deze zelfondertekende certificaten SHA-256 en hebben ze een sleutellengte van 2048 bits. Voor Windows Server 2003 wordt SHA1 gebruikt met een sleutellengte van 1024 bits. Als deze zelfondertekende certificaten verdacht zijn, blokkeer dan, om kwaadwillende personen te beletten om ze te gebruiken om vertrouwde clients te imiteren, de certificaten in het knooppunt **Certificaten** in de werkruimte **Beheer** , knooppunt **Veiligheid** .  

### <a name="client-and-server-authentication"></a>Client-en Server verificatie  
 Wanneer clients verbinding maken via HTTP, verifiëren ze de beheer punten met behulp van een Active Directory Domain Services of met behulp van de Configuration Manager vertrouwde basis sleutel. Clients verifiëren geen andere systeemsite-functies, zoals statusmigratiepunten of software-updatepunten.  

 Indien een beheerpunt eerst een client verifieert door de zelfondertekende client-certificaten te gebruiken, voorziet dit mechanisme minimale veiligheid omdat elke computer zelfondertekende certificaten kan genereren. In dit scenario moet het client-identificatieproces versterkt worden door goedkeuring. Alleen vertrouwde computers moeten worden goedgekeurd, hetzij automatisch door Configuration Manager, hetzij hand matig, door een gebruiker met beheerders rechten. Zie de sectie goed keuring in [communicatie tussen eind punten](../hierarchy/communications-between-endpoints.md)voor meer informatie.  

## <a name="about-ssl-vulnerabilities"></a>Over SSL-beveiligings problemen
Ga als volgt te werk om de beveiliging van uw Configuration Manager-clients en-servers te verbeteren:

- TLS 1.2 inschakelen

  Zie [tls 1,2 inschakelen voor Configuration Manager](enable-tls-1-2.md)om TLS 1,2 in te scha kelen voor Configuration Manager.
- SSL 3,0, TLS 1,0 en TLS 1,1 uitschakelen 
- De aan TLS gerelateerde coderings suites opnieuw ordenen 

Zie [het gebruik van bepaalde cryptografische algoritmen en protocollen in Schannel.dll](https://support.microsoft.com/help/245030/) en [prioriteiten voor Schannel-coderings suites](https://docs.microsoft.com/windows/win32/secauthn/prioritizing-schannel-cipher-suites)beperken voor meer informatie. Deze procedures hebben geen invloed op de functionaliteit van Configuration Manager.

