---
title: Beveiliging en privacy voor site beheer
titleSuffix: Configuration Manager
description: Optimaliseer beveiliging en privacy voor site beheer in Configuration Manager
ms.date: 04/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 923018e35fae1ec1f5e9c0869ef22d43b5de552b
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/28/2020
ms.locfileid: "82182256"
---
# <a name="security-and-privacy-for-site-administration-in-configuration-manager"></a>Beveiliging en privacy voor site beheer in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit artikel bevat beveiligings-en privacy-informatie voor Configuration Manager-sites en de hiërarchie.

## <a name="security-guidance-for-site-administration"></a><a name="BKMK_Security_Sites"></a>Beveiligings richtlijnen voor site beheer

Gebruik de volgende richt lijnen om u te helpen bij het beveiligen van Configuration Manager-sites en de hiërarchie.  

### <a name="run-setup-from-a-trusted-source-and-secure-communication"></a>Setup uitvoeren vanuit een vertrouwde bron en beveiligde communicatie

U kunt voor komen dat iemand met de bron bestanden knoeit door Configuration Manager Setup uit te voeren vanaf een vertrouwde bron. Slaat u bestanden op het netwerk op, dan beveiligt u de netwerklocatie.  

Als u Setup vanaf een netwerk locatie uitvoert, om te voor komen dat een kwaadwillende persoon knoeit met de bestanden die via het netwerk worden verzonden, gebruikt u IPsec of SMB-ondertekening tussen de bron locatie van de installatie bestanden en de site server.  

Als u het download programma voor de installatie gebruikt om de bestanden te downloaden die vereist zijn voor de installatie, moet u ervoor zorgen dat u de locatie beveiligt waar deze bestanden worden opgeslagen. Beveilig ook het communicatie kanaal voor deze locatie wanneer u het installatie programma uitvoert.  

### <a name="extend-the-active-directory-schema-and-publish-sites-to-the-domain"></a>Het Active Directory schema uitbreiden en sites publiceren naar het domein  

Schema-uitbrei dingen zijn niet vereist om Configuration Manager uit te voeren, maar ze maken een veiligere omgeving. Clients en site servers kunnen informatie ophalen van een vertrouwde bron.  

Als clients zich in een niet-vertrouwd domein bevinden, implementeert u de volgende site systeem rollen in de domeinen van de clients:  

- Beheerpunt  

- Distributiepunt  

> [!NOTE]  
> Een vertrouwd domein voor Configuration Manager vereist Kerberos-verificatie. Als clients zich in een ander forest bevinden dat geen twee richtings vertrouwensrelatie heeft met het forest van de site server, worden deze clients geacht zich in een niet-vertrouwd domein te bevinden. Een externe vertrouwens relatie is niet voldoende voor dit doel.  

### <a name="use-ipsec-to-secure-communications"></a>IPsec gebruiken om de communicatie te beveiligen

Hoewel Configuration Manager beveiligde communicatie tussen de site server en de computer met SQL Server, Configuration Manager beveiligt de communicatie tussen site systeem rollen en SQL Server niet. U kunt sommige site systemen alleen configureren met HTTPS voor intra site-communicatie.  

Als u geen extra besturings elementen gebruikt om deze server-naar-server-kanalen te beveiligen, kunnen aanvallers verschillende spoofing-en man-in-the-middle-aanvallen gebruiken tegen site systemen. Gebruik SMB-ondertekening wanneer u IPsec niet kunt gebruiken.  

> [!Important]  
> Beveilig het communicatie kanaal tussen de site server en de bron server van het pakket. Deze communicatie maakt gebruik van SMB. Als u IPsec niet kunt gebruiken om deze communicatie te beveiligen, gebruikt u SMB-ondertekening om ervoor te zorgen dat er niet met de bestanden wordt geknoeid voordat clients ze downloaden en uitvoeren.  

### <a name="dont-change-the-default-security-groups"></a>Wijzig de standaard beveiligings groepen niet

Wijzig de volgende beveiligings groepen die Configuration Manager maakt en beheert voor site systeem communicatie:

- **SMS_SiteSystemToSiteServerConnection_MP_&lt;site code\>**  

- **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;site code\>**  

- **SMS_SiteSystemToSiteServerConnection_Stat_&lt;site code\>**  

Configuration Manager maakt en beheert deze beveiligings groepen automatisch. Dit gedrag omvat het verwijderen van computer accounts wanneer een site systeemrol wordt verwijderd.  

Bewerk deze groepen niet hand matig om te controleren of de continuïteit van de service en de minimale bevoegdheden.  

### <a name="manage-the-trusted-root-key-provisioning-process"></a>Het inrichtings proces van de vertrouwde basis sleutel beheren

Als clients de globale catalogus voor Configuration Manager informatie niet kunnen opvragen, moeten ze vertrouwen op de vertrouwde basis sleutel om geldige beheer punten te verifiëren. De vertrouwde basis sleutel wordt opgeslagen in het client register. Het kan worden ingesteld met behulp van groeps beleid of hand matige configuratie.  

Als de client geen kopie van de vertrouwde basis sleutel heeft voordat deze voor de eerste keer contact opneemt met een beheer punt, wordt het eerste beheer punt vertrouwd waarmee wordt gecommuniceerd. U kunt de clients vooraf inrichten door gebruik te maken van de vertrouwde basissleutel om het risico te verkleinen dat een aanvaller clients naar een niet-geautoriseerd beheerpunt omleidt. Zie [planning voor de vertrouwde basis sleutel](../security/plan-for-security.md#BKMK_PlanningForRTK)voor meer informatie.  

### <a name="use-non-default-port-numbers"></a>Niet-standaard poort nummers gebruiken

Het gebruik van niet-standaard poort nummers kan extra beveiliging bieden. Ze maken het moeilijker voor aanvallers om de omgeving in voor bereiding voor een aanval te verkennen. Als u besluit om niet-standaard poorten te gebruiken, moet u deze plannen voordat u Configuration Manager installeert. Gebruik ze consistent op alle sites in de hiërarchie. Poorten voor client aanvragen en Wake On LAN zijn voor beelden waarin u niet-standaard poort nummers kunt gebruiken.  

### <a name="use-role-separation-on-site-systems"></a>Functie scheiding op site systemen gebruiken

Hoewel u alle site systeem rollen op één computer kunt installeren, wordt deze praktijk zelden gebruikt op productie netwerken. Er wordt een Single Point of Failure gemaakt.  

### <a name="reduce-the-attack-profile"></a>Verminder het aanvals profiel

Het isoleren van elke site systeemrol op een andere server verkleint de kans dat een aanval op beveiligings problemen op één site systeem kan worden gebruikt op een ander site systeem. Voor veel rollen is de installatie van Internet Information Services (IIS) op het site systeem vereist. dit vereist de kwets baarheid. Als u rollen moet combi neren om de hardware-uitgaven te verminderen, kunt u IIS-rollen alleen combi neren met andere rollen waarvoor IIS is vereist.  

> [!IMPORTANT]  
> De rol van het terugval status punt is een uitzonde ring. Omdat deze site systeemrol niet-geverifieerde gegevens van clients accepteert, moet u de rol van het terugval status punt niet toewijzen aan een andere Configuration Manager-site systeemrol.  

### <a name="configure-static-ip-addresses-for-site-systems"></a>Statische IP-adressen voor site systemen configureren

Statische IP-adressen zijn gemakkelijker te beschermen tegen aanvallen met naamomzetting.  

Statische IP-adressen maken ook de configuratie van IPsec eenvoudiger. Het gebruik van IPsec is een beveiligings best practice voor het beveiligen van de communicatie tussen site systemen in Configuration Manager.  

### <a name="dont-install-other-applications-on-site-system-servers"></a>Installeer geen andere toepassingen op site systeem servers

Wanneer u andere toepassingen op site systeem servers installeert, verhoogt u de kwets baarheid voor Configuration Manager. Er zijn ook problemen met de compatibiliteit.  

### <a name="require-signing-and-enable-encryption-as-a-site-option"></a>Ondertekening vereisen en versleuteling inschakelen als een optie voor een site

Schakel de ondertekenings- en versleutelingsopties voor de site in. Zorg ervoor dat alle clients het hash-algoritme SHA-256 kunnen ondersteunen en schakel vervolgens de optie in voor het **vereisen van SHA-256**.  

### <a name="restrict-and-monitor-administrative-users"></a>Gebruikers met beheerders rechten beperken en bewaken

Verleen beheerders toegang tot Configuration Manager alleen voor gebruikers die u vertrouwt. Ken hen vervolgens minimale machtigingen toe door de ingebouwde beveiligings rollen te gebruiken of door de beveiligings rollen aan te passen. Gebruikers met beheerders rechten die software en configuraties kunnen maken, wijzigen en implementeren, kunnen mogelijk apparaten best uren in de Configuration Manager-hiërarchie.  

Controleer regelmatig de toewijzingen van gebruikers met beheerdersrechten en hun autorisatieniveau om de vereiste wijzigingen te verifiëren.  

Zie [op rollen gebaseerd beheer configureren](../../servers/deploy/configure/configure-role-based-administration.md)voor meer informatie.  

### <a name="secure-configuration-manager-backups"></a>Configuration Manager back-ups beveiligen

Wanneer u een back-up maakt van Configuration Manager, omvat deze informatie certificaten en andere gevoelige gegevens die door een aanvaller kunnen worden gebruikt voor imitatie.  

Gebruik SMB-ondertekening of IPsec wanneer u gegevens via het netwerk overdraagt en beveilig de locatie van back-up.  

### <a name="secure-locations-for-exported-objects"></a>Beveiligde locaties voor geëxporteerde objecten

Wanneer u objecten exporteert of importeert van de Configuration Manager-console naar een netwerk locatie, Beveilig de locatie en Beveilig het netwerk kanaal.

Beperk wie toegang heeft tot de netwerkmap.  

Gebruik SMB-ondertekening of IPsec tussen de netwerk locatie en de site server om te voor komen dat een kwaadwillende persoon knoeit met de geëxporteerde gegevens. Beveilig ook de communicatie tussen de computer waarop de Configuration Manager-console en de site server worden uitgevoerd. Gebruik IPsec om de gegevens op het netwerk te versleutelen om openbaarmaking van informatie te voorkomen.  

### <a name="manually-remove-certificates-from-failed-servers"></a>Certificaten hand matig verwijderen van servers waarop de fout is opgetreden

Als een site systeem niet goed wordt verwijderd of niet meer werkt en niet kan worden hersteld, verwijdert u hand matig de Configuration Manager certificaten voor deze server van andere Configuration Manager-servers.

Als u de peer vertrouwensrelatie wilt verwijderen die oorspronkelijk tot stand is gebracht met het site systeem en de site systeem rollen, verwijdert u hand matig de Configuration Manager-certificaten voor de server met een fout in het **vertrouwde personen** -certificaat archief op andere site systeem servers. Deze actie is belang rijk als u de server opnieuw gebruikt zonder deze opnieuw in te delen.  

Zie voor meer informatie [cryptografische besturings elementen voor Server communicatie](../security/cryptographic-controls-technical-reference.md#cryptographic-controls-for-server-communication).  

### <a name="dont-configure-internet-based-site-systems-to-bridge-the-perimeter-network"></a>Configureer geen site systemen op internet om het perimeter netwerk te bridgen

Configureer site systeem servers niet op meerdere locaties zodat ze verbinding maken met het perimeter netwerk en het intranet. Hoewel deze configuratie internet-gebaseerde site systemen toestaat client verbindingen van het internet en het intranet te accepteren, wordt er een beveiligings grens tussen het perimeter netwerk en het intranet geëlimineerd.  

### <a name="configure-the-site-server-to-initiate-connections-to-perimeter-networks"></a>De site server configureren voor het initiëren van verbindingen met perimeter netwerken

Als een site systeem zich in een niet-vertrouwd netwerk bevindt, zoals een perimeter netwerk, configureert u de site server om verbindingen met het site systeem te initiëren.

Standaard initiëren site systemen verbindingen met de site server om gegevens over te dragen. Deze configuratie kan een beveiligings risico vormen wanneer het initiëren van de verbinding van een niet-vertrouwd netwerk naar het vertrouwde netwerk. Wanneer site systemen verbindingen van het Internet accepteren of zich in een niet-vertrouwd forest bevinden, configureert u de site systeem optie om te **vereisen dat de site server verbindingen met dit site systeem initieert**. Na de installatie van het site systeem en alle rollen, worden alle verbindingen geïnitieerd door de site server van het vertrouwde netwerk.  

### <a name="use-ssl-bridging-and-termination-with-authentication"></a>SSL-bridging en-beëindiging met verificatie gebruiken

Als u een webproxyserver gebruikt voor client beheer op internet, gebruikt u SSL-bridging naar SSL, met behulp van beëindigen met verificatie.

Wanneer u SSL-beëindiging op de proxy webserver configureert, zijn pakketten van het Internet onderhevig aan inspectie voordat ze worden doorgestuurd naar het interne netwerk. De proxy webserver verifieert de verbinding van de client, beëindigt deze en opent vervolgens een nieuwe geverifieerde verbinding met de site systemen op internet.  

Als Configuration Manager-client computers een proxy webserver gebruiken om verbinding te maken met site systemen op internet, is de client identiteit (GUID) beveiligd in de pakket lading. Vervolgens beschouwt het beheer punt de proxy webserver niet als de client.

Als uw proxy webserver de vereisten voor SSL-bridging niet kan ondersteunen, wordt ook SSL-Tunneling ondersteund. Deze optie is minder veilig. De SSL-pakketten van het Internet worden doorgestuurd naar de site systemen zonder beëindiging. Vervolgens kunnen ze niet worden geïnspecteerd op schadelijke inhoud.  

> [!WARNING]  
> Mobiele apparaten die zijn Inge schreven door Configuration Manager, kunnen geen gebruikmaken van SSL-bridging. Ze moeten alleen SSL-Tunneling gebruiken.  

### <a name="configurations-to-use-if-you-configure-the-site-to-wake-up-computers-to-install-software"></a>Te gebruiken configuraties als u de site configureert om computers te activeren om software te installeren

- Als u traditionele Ontwaak pakketten gebruikt, gebruikt u unicast in plaats van subnet gerichte broadcasts.  

- Als u op het subnet gerichte broadcasts moet gebruiken, configureert u routers om alleen IP-gerichte broadcasts toe te staan vanaf de site server en alleen voor een niet-standaard poort nummer.  

Zie [planning How to wake up clients](../../clients/deploy/plan/plan-wake-up-clients.md)(Engelstalig) voor meer informatie over de verschillende Wake on LAN technologieën.

### <a name="if-you-use-email-notification-configure-authenticated-access-to-the-smtp-mail-server"></a>Configureer geverifieerde toegang tot de SMTP-mail server als u e-mail meldingen gebruikt.

Gebruik, indien mogelijk, een e-mail server die geverifieerde toegang ondersteunt. Gebruik het computer account van de site server voor verificatie. Gebruik het account met de minste bevoegdheden als u een gebruikersaccount moet opgeven voor verificatie. 

### <a name="enforce-ldap-channel-binding-and-ldap-signing"></a>LDAP-kanaal binding en LDAP-ondertekening afdwingen

De beveiliging van Active Directory domein controllers kan worden verbeterd door de server te configureren voor het afwijzen van LDAP-bindingen Simple Authentication and Security Layer (SASL) die geen ondertekening aanvragen of om LDAP-eenvoudige bindingen af te wijzen die worden uitgevoerd op een normale tekst verbinding. Vanaf versie 1910 biedt Configuration Manager ondersteuning voor het afdwingen van LDAP-kanaal binding en LDAP-ondertekening. Zie [2020 LDAP-kanaal binding en vereisten voor LDAP-ondertekening voor Windows](https://support.microsoft.com/help/4520412/2020-ldap-channel-binding-and-ldap-signing-requirements-for-windows)voor meer informatie. <!--6244453-->


## <a name="security-guidance-for-the-site-server"></a><a name="BKMK_Security_SiteServer"></a>Beveiligings richtlijnen voor de site server

Gebruik de volgende richt lijnen om u te helpen de Configuration Manager-site server te beveiligen.  

### <a name="install-configuration-manager-on-a-member-server-instead-of-a-domain-controller"></a>Configuration Manager installeren op een lidserver in plaats van een domein controller

De Configuration Manager-site server en-site systemen hoeven niet te worden geïnstalleerd op een domein controller. Domein controllers hebben geen lokale SAM-data base (Security Accounts Management) dan de domein database. Wanneer u Configuration Manager op een lidserver installeert, kunt u Configuration Manager accounts in de lokale SAM-data base behouden in plaats van de domein database.  

Deze procedure verlaagt ook de kwetsbaarheid op uw domeincontrollers.  

### <a name="install-secondary-sites-without-copying-the-files-over-the-network"></a>Secundaire sites installeren zonder de bestanden via het netwerk te kopiëren

Wanneer u Setup uitvoert en een secundaire site maakt, selecteert u niet de optie om de bestanden van de bovenliggende site naar de secundaire site te kopiëren. Gebruik ook geen netwerk bron locatie. Wanneer u bestanden over het netwerk kopieert, zou een ervaren aanvaller het installatie pakket van de secundaire site kunnen overnemen en knoeien met de bestanden voordat ze worden geïnstalleerd. Het kan lastig zijn om deze aanval in te richten. Deze aanval kan worden voorkomen door IPsec of SMB te gebruiken voor de bestandsoverdracht.  

In plaats van het kopiëren van de bestanden via het netwerk, kopieert u op de secundaire site server de bron bestanden uit de map media naar een lokale map. Wanneer u vervolgens Setup uitvoert om een secundaire site te maken, selecteert u op de pagina **bron bestanden voor installatie** **de optie de bron bestanden op de volgende locatie op de secundaire site computer gebruiken (veiligst)** en geeft u deze map op.  

Zie [een secundaire site installeren](../../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary)voor meer informatie.

### <a name="site-role-installation-inherits-permissions-from-drive-root"></a>De installatie van de site functie neemt machtigingen over van de hoofdmap van het station

<!-- SCCMDocs#1380 -->
Zorg ervoor dat u de machtigingen voor het systeem station correct configureert voordat u de eerste site systeemrol op een server installeert. `C:\SMS_CCM` Neemt bijvoorbeeld machtigingen over van `C:\`. Als de hoofdmap van het station niet goed is beveiligd, kunnen gebruikers met beperkte rechten mogelijk inhoud in de map Configuration Manager openen of wijzigen.


## <a name="security-guidance-for-sql-server"></a><a name="BKMK_Security_SQLServer"></a>Beveiligings richtlijnen voor SQL Server

Configuration Manager gebruikt SQL Server als de back-enddatabase. Als de data base is aangetast, kunnen aanvallers Configuration Manager overs Laan. Als ze rechtstreeks toegang SQL Server, kunnen ze via Configuration Manager aanvallen starten. Overweeg aanvallen tegen SQL Server een hoog risico en een oplossing te bieden.  

Gebruik de volgende beveiligings richtlijnen om u te helpen bij het beveiligen van SQL Server voor Configuration Manager.  

### <a name="dont-use-the-configuration-manager-site-database-server-to-run-other-sql-server-applications"></a>Gebruik niet de Configuration Manager-site database server om andere SQL Server-toepassingen uit te voeren

Wanneer u de toegang tot de Configuration Manager site database server verhoogt, neemt deze actie het risico voor uw Configuration Manager gegevens toe. Als de Configuration Manager-site database is aangetast, zijn andere toepassingen op dezelfde SQL Server computer ook kwetsbaar.  

### <a name="configure-sql-server-to-use-windows-authentication"></a>SQL Server configureren voor het gebruik van Windows-verificatie

Hoewel Configuration Manager toegang krijgt tot de site database met behulp van een Windows-account en Windows-verificatie, is het nog steeds mogelijk om SQL Server te configureren voor gebruik van SQL Server gemengde modus. Met SQL Server gemengde modus kunnen extra SQL-aanmeldingen worden uitgevoerd voor toegang tot de data base. Deze configuratie is niet vereist en verhoogt de kwets baarheid voor aanvallen.  

### <a name="update-sql-server-express-at-secondary-sites"></a>SQL Server Express bijwerken op secundaire sites

Wanneer u een primaire site installeert, Configuration Manager down loads SQL Server Express vanuit het micro soft Download centrum. Vervolgens worden de bestanden naar de primaire site server gekopieerd. Wanneer u een secundaire site installeert en de optie selecteert waarmee SQL Server Express wordt geïnstalleerd, wordt Configuration Manager de eerder gedownloade versie geïnstalleerd. Er wordt niet gecontroleerd of er nieuwe versies beschikbaar zijn. Voer een van de volgende taken uit om ervoor te zorgen dat de secundaire site de meest recente versies heeft:  

- Nadat u de secundaire site hebt geïnstalleerd, voert u Windows Update uit op de secundaire site server.  

- Voordat u de secundaire site installeert, moet u SQL Server Express hand matig installeren op de secundaire site server. Zorg ervoor dat u de meest recente versie en eventuele software-updates installeert. Installeer vervolgens de secundaire site en selecteer de optie om een bestaand SQL Server exemplaar te gebruiken.  

Voer regel matig Windows Update uit voor alle geïnstalleerde versies van SQL Server. Deze procedure zorgt ervoor dat ze de meest recente software-updates hebben.  

### <a name="follow-general-guidance-for-sql-server"></a>Volg de algemene richt lijnen voor SQL Server

Bepaal en volg de algemene richt lijnen voor uw versie van SQL Server. Houd echter rekening met de volgende vereisten voor Configuration Manager:  

- Het computeraccount van de siteserver moet lid zijn van de groep Beheerders op de computer waar SQL Server op wordt uitgevoerd. Als u de SQL Server aanbeveling van ' inrichtende beheerders principals ' expliciet volgt, moet het account dat u gebruikt om het installatie programma uit te voeren op de site server lid zijn van de groep SQL-gebruikers.  

- Als u SQL Server installeert met behulp van een domein gebruikers account, moet u ervoor zorgen dat het computer account van de site server is geconfigureerd voor een SPN (Service Principal Name) die is gepubliceerd naar Active Directory Domain Services. Zonder de SPN mislukt de Kerberos-verificatie en Configuration Manager Setup mislukt.  


## <a name="security-guidance-for-site-systems-that-run-iis"></a><a name="BKMK_Security_IIS"></a>Beveiligings richtlijnen voor site systemen die IIS uitvoeren

IIS is vereist voor verschillende site systeem rollen in Configuration Manager. Het proces van het beveiligen van IIS zorgt ervoor dat Configuration Manager correct werkt en het risico op beveiligings aanvallen vermindert. Minimaliseer zo handig het aantal servers waarvoor IIS is vereist. Voer bijvoorbeeld alleen het aantal beheer punten uit dat u nodig hebt om de client basis te ondersteunen, waarbij u rekening houdt met hoge Beschik baarheid en netwerk isolatie voor client beheer op internet.  

Gebruik de volgende richt lijnen om u te helpen bij het beveiligen van de site systemen waarop IIS wordt uitgevoerd.  

### <a name="disable-iis-functions-that-you-dont-require"></a>Schakel IIS-functies uit die u niet nodig hebt

Installeer alleen de IIS-functies die u nodig hebt voor de sitesysteemrol die u installeert. Zie voor meer informatie [Site and site system prerequisites](../configs/site-and-site-system-prerequisites.md) (Vereisten voor sites en sitesystemen).  

### <a name="configure-the-site-system-roles-to-require-https"></a>De site systeem rollen configureren om HTTPS te vereisen

Wanneer clients verbinding maken met een site systeem via HTTP in plaats van met behulp van HTTPS, gebruiken ze Windows-verificatie. Dit gedrag kan worden terugvallen op het gebruik van NTLM-verificatie in plaats van Kerberos-verificatie. Als NTLM-verificatie wordt gebruikt, is het mogelijk dat clients verbinden met een rogue server.  

De uitzonde ring op deze richt lijnen kan distributie punten zijn. Pakket toegangs accounts werken niet wanneer het distributie punt is geconfigureerd voor HTTPS. Pakkettoegangsaccounts geven goedkeuring aan de inhoud; zo kunt u beperken welke gebruikers toegang hebben tot de inhoud. Zie [aanbevolen beveiligings procedures voor inhouds beheer](security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement)voor meer informatie.  

### <a name="configure-a-certificate-trust-list-ctl-in-iis-for-site-system-roles"></a>Een certificaat vertrouwens lijst (CTL) in IIS configureren voor site systeem rollen

Sitesysteemrollen:  

- Een distributie punt dat u configureert voor HTTPS  

- Een beheer punt dat u configureert voor HTTPS en ondersteuning voor mobiele apparaten inschakelt

Een CTL is een gedefinieerde lijst met vertrouwde basis certificerings instanties (Ca's). Wanneer u een CTL gebruikt met groeps beleid en een implementatie van een open bare-sleutel infrastructuur (PKI), kunt u met een CTL een aanvulling vormen op de bestaande vertrouwde basis certificerings instanties die in uw netwerk zijn geconfigureerd. Bijvoorbeeld Ca's die automatisch worden geïnstalleerd met micro soft Windows of worden toegevoegd via Windows Enter prise root CAs. Wanneer een CTL in IIS is geconfigureerd, wordt een subset van deze vertrouwde basis certificerings instanties gedefinieerd.  

Deze subset biedt u meer controle over de beveiliging. De CTL beperkt de client certificaten die alleen worden geaccepteerd voor certificaten die zijn verleend uit de lijst met certificerings instanties in de CTL. Windows wordt bijvoorbeeld geleverd met een aantal bekende certificaten van certificerings instanties van derden, zoals VeriSign en Thawte.

Standaard vertrouwt de computer die IIS uitvoert, certificaten die zijn gekoppeld aan deze bekende certificerings instanties. Wanneer u IIS niet configureert met een CTL voor de vermelde site systeem rollen, accepteert de site als een geldige client elk apparaat met een certificaat dat is uitgegeven door deze certificerings instanties. Als u IIS configureert met een CTL die deze certificerings instanties niet bevat, worden de client verbindingen door de site geweigerd als het certificaat aan deze certificerings instanties wordt gekoppeld. Als u wilt dat Configuration Manager-clients worden geaccepteerd voor de vermelde site systeem rollen, moet u IIS configureren met een CTL waarmee de Ca's worden opgegeven die worden gebruikt door Configuration Manager-clients.  

> [!NOTE]  
> Alleen voor de vermelde site systeem rollen moet u een CTL configureren in IIS. De lijst met certificaat verleners die Configuration Manager gebruikt voor beheer punten, biedt dezelfde functionaliteit voor client computers wanneer ze verbinding maken met HTTPS-beheer punten.  

Zie de IIS-documentatie voor meer informatie over het configureren van een lijst met vertrouwde certificerings instanties in IIS.  

### <a name="dont-put-the-site-server-on-a-computer-with-iis"></a>Plaats de site server niet op een computer met IIS

Functiescheiding helpt de kwetsbaarheid te verlagen en de herstelmogelijkheden te verbeteren. Het computer account van de site server heeft doorgaans beheerders bevoegdheden op alle site systeem rollen. Het kan ook deze bevoegdheden hebben op Configuration Manager-clients, als u client push installatie gebruikt.  

### <a name="use-dedicated-iis-servers-for-configuration-manager"></a>Speciale IIS-servers gebruiken voor Configuration Manager

Hoewel u meerdere webtoepassingen kunt hosten op de IIS-servers die ook door Configuration Manager worden gebruikt, kan deze praktijk uw kwets baarheid aanzienlijk verhogen. Een slecht geconfigureerde toepassing kan een aanvaller in staat stellen om de controle over een Configuration Manager-site systeem te krijgen. Deze schending kan een aanvaller in staat stellen om de controle over de hiërarchie te krijgen.  

Als u andere webtoepassingen moet uitvoeren op Configuration Manager-site systemen, maakt u een aangepaste website voor Configuration Manager site systemen.  

### <a name="use-a-custom-website"></a>Een aangepaste website gebruiken

Voor site systemen die IIS uitvoeren, configureert u Configuration Manager voor het gebruik van een aangepaste website in plaats van de standaard website. Als u andere webtoepassingen op het site systeem wilt uitvoeren, moet u een aangepaste website gebruiken. Deze instelling is een instelling voor de hele site in plaats van een instelling voor een specifiek site systeem.  

### <a name="when-you-use-custom-websites-remove-the-default-virtual-directories"></a>Wanneer u aangepaste websites gebruikt, verwijdert u de virtuele standaard mappen

Wanneer u overschakelt van het gebruik van de standaard website naar een aangepaste website, Configuration Manager verwijdert u de oude virtuele mappen niet. Verwijder de virtuele mappen die Configuration Manager oorspronkelijk is gemaakt op de standaard website.  

Verwijder bijvoorbeeld de volgende virtuele mappen voor een distributie punt:  

- SMS_DP_SMSPKG$  

- SMS_DP_SMSSIG$  

- NOCERT_SMS_DP_SMSPKG$  

- NOCERT_SMS_DP_SMSSIG$  

### <a name="follow-iis-server-security-guidance"></a>Volg de richt lijnen voor IIS Server-beveiliging

Bepaal en volg de algemene richt lijnen voor uw versie van IIS server. Houd rekening met de vereisten die Configuration Manager voor specifieke site systeem rollen heeft. Zie voor meer informatie [Site and site system prerequisites](../configs/site-and-site-system-prerequisites.md) (Vereisten voor sites en sitesystemen).  


## <a name="security-guidance-for-the-management-point"></a><a name="BKMK_Security_ManagementPoint"></a>Beveiligings richtlijnen voor het beheer punt

Beheer punten zijn de primaire interface tussen apparaten en Configuration Manager. Overweeg aanvallen tegen het beheer punt en de server waarop deze wordt uitgevoerd, een hoog risico te bieden en de juiste oplossing te bieden. Pas alle toepasselijke beveiligings richtlijnen en monitor voor ongebruikelijke activiteiten toe.  

Gebruik de volgende richt lijnen om een beheer punt in Configuration Manager te beveiligen.  

### <a name="assign-the-client-on-a-management-point-to-the-same-site"></a>De client op een beheer punt toewijzen aan dezelfde site

Vermijd het scenario waarin u de Configuration Manager-client die zich op een beheer punt bewaart, toewijst aan een andere site dan de site van het beheer punt.  

Als u van een eerdere versie migreert naar Configuration Manager huidige vertakking, migreert u zo snel mogelijk de client op het beheer punt naar de nieuwe site.  


## <a name="security-guidance-for-the-fallback-status-point"></a><a name="BKMK_Security_FSP"></a>Beveiligings richtlijnen voor het terugval status punt

Als u een terugval status punt in Configuration Manager installeert, gebruikt u de volgende beveiligings richtlijnen:

Zie [bepalen of u een terugval status punt nodig hebt](../../clients/deploy/plan/determine-the-site-system-roles-for-clients.md#fallback-status-point)voor meer informatie over de beveiligings overwegingen wanneer u een terugval status punt installeert.  

### <a name="dont-run-any-other-roles-on-the-same-site-system"></a>Geen andere rollen uitvoeren op hetzelfde site systeem

Het terugval status punt is ontworpen om niet-geverifieerde communicatie van een wille keurige computer te accepteren. Als u deze site systeemrol uitvoert met andere rollen of een domein controller, neemt het risico op die server aanzienlijk toe.  

### <a name="install-the-fallback-status-point-before-you-install-clients-with-pki-certificates"></a>Installeer het terugval status punt voordat u clients installeert met PKI-certificaten

Als Configuration Manager-site systemen geen HTTP-client communicatie accepteren, bent u mogelijk niet op de hoogte dat clients niet-beheerd zijn wegens PKI-gerelateerde certificaat problemen. Als u clients toewijst aan een terugval status punt, rapporteren ze deze certificaat problemen via het terugval status punt.  

Uit veiligheids overwegingen kunt u geen terugval status punt toewijzen aan clients nadat ze zijn geïnstalleerd. U kunt deze rol alleen toewijzen tijdens de client installatie.  

### <a name="avoid-using-the-fallback-status-point-in-the-perimeter-network"></a>Vermijd het gebruik van het terugval status punt in het perimeter netwerk

Het terugvalstatuspunt is bedoeld om gegevens van elke client te accepteren. Hoewel een terugval status punt in het perimeter netwerk u kan helpen bij het oplossen van problemen met clients op internet, kunt u de voor delen van het oplossen van problemen in balans brengen met het risico van een site systeem dat niet-geverifieerde gegevens accepteert in een openbaar toegankelijk netwerk.  

Als u het terugval status punt in het perimeter netwerk of een niet-vertrouwd netwerk installeert, configureert u de site server om gegevens overdrachten te initiëren. Gebruik niet de standaard instelling die het terugval status punt toestaat een verbinding met de site server te initiëren.  


## <a name="security-issues-for-site-administration"></a><a name="BKMK_SecurityIssues_Clients"></a>Beveiligings problemen voor site beheer

Bekijk de volgende beveiligings problemen voor Configuration Manager:  

- Configuration Manager heeft geen bescherming tegen een geautoriseerde gebruiker met beheerders rechten die gebruikmaakt van Configuration Manager om het netwerk aan te vallen. Niet-geautoriseerde gebruikers met beheerders rechten vormen een hoog beveiligings risico. Ze kunnen veel aanvallen starten, waaronder de volgende strategieën:  

    - Gebruik software-implementatie om automatisch schadelijke software te installeren en uit te voeren op elke Configuration Manager-client computer in de organisatie.  

    - Een Configuration Manager client op afstand beheren zonder toestemming van de client.  

    - Configureer snelle polling intervallen en extreme hoeveel heden inventarisatie. Deze actie maakt Denial-of-service-aanvallen tegen de clients en servers.  

    - Eén site in de hiërarchie gebruiken om gegevens naar Active Directory-gegevens van een andere site te schrijven.  

    De site hiërarchie is de beveiligings grens. Houd er rekening mee dat sites alleen beheer grenzen hebben.  

    Controleer de gehele activiteit van gebruikers met beheerdersrechten en controleer regelmatig de controlelogboeken. Vereisen dat alle Configuration Manager gebruikers met beheerders rechten een achtergrond controle ondergaan voordat ze worden ingehuurd. Periodieke recontroles vereisen als werkings voorwaarde.  

- Als er is geknoeid met het inschrijvings punt, kan een aanvaller certificaten voor verificatie verkrijgen. Ze kunnen de referenties van gebruikers die hun mobiele apparaten inschrijven, stelen.  

    Het registratie punt communiceert met een certificerings instantie. U kunt hiermee Active Directory-objecten maken, wijzigen en verwijderen. Installeer het inschrijvings punt nooit in het perimeter netwerk. Altijd controleren op ongebruikelijke activiteiten.  

- Als u gebruikers beleid toestaat voor client beheer op internet, kunt u uw aanvals profiel verhogen.  

    Naast het gebruik van PKI-certificaten voor client-naar-server-verbindingen, is voor deze configuraties Windows-verificatie vereist. Ze kunnen terugvallen op het gebruik van NTLM-verificatie in plaats van Kerberos. NTLM-verificatie is kwetsbaar voor imitatie- en replayaanvallen. Als u een gebruiker op het Internet wilt verifiëren, moet u een verbinding van het site systeem op internet naar een domein controller toestaan.  

- De **admin $** -share is vereist op site systeem servers.  

    De Configuration Manager-site server gebruikt de admin $-share om verbinding te maken met en bewerkingen uit te voeren op site systemen. Schakel deze share niet uit of verwijder deze.  

- Configuration Manager maakt gebruik van naamomzettingsservices om verbinding te maken met andere computers. Deze services zijn moeilijk te beveiligen tegen de volgende beveiligings aanvallen:
    - Adresvervalsing (spoofing)
    - Knoeien
    - Ging
    - Vrijgeven van informatie
    - Denial of Service
    - Uitbrei ding van bevoegdheden

    Bepaal en volg alle beveiligings richtlijnen voor de DNS-versie die u voor naam omzetting gebruikt.  

## <a name="privacy-information-for-discovery"></a><a name="BKMK_Privacy_Cliients"></a>Privacy-informatie voor detectie

Detectie maakt records voor netwerk bronnen en slaat deze op in de Configuration Manager-Data Base. Detectie gegevens records bevatten computer gegevens zoals IP-adressen, versies van besturings systemen en computer namen. U kunt ook Active Directory detectie methoden configureren om informatie te retour neren die uw organisatie in Active Directory Domain Services opslaat.  

De enige detectie methode die Configuration Manager standaard is ingeschakeld is heartbeat-detectie. Deze methode detecteert alleen computers waarop de Configuration Manager-client software al is geïnstalleerd.  

Detectie gegevens worden niet rechtstreeks naar micro soft verzonden. Deze wordt opgeslagen in de Configuration Manager-Data Base. Configuration Manager behoudt informatie in de data base totdat de gegevens worden verwijderd. Dit proces wordt om de 90 dagen uitgevoerd door de taak site onderhoud **verouderde detectie gegevens verwijderen**.  
