---
title: De communicatie tussen de eindpunten
titleSuffix: Configuration Manager
description: Meer informatie over hoe Configuration Manager-site systemen en-onderdelen via een netwerk communiceren.
ms.date: 10/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0f60d268e1f9bfad9c062041e810be2092da5508
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587234"
---
# <a name="communications-between-endpoints-in-configuration-manager"></a>De communicatie tussen de eind punten in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel wordt beschreven hoe Configuration Manager-site systemen en-clients via uw netwerk communiceren. De sectie bevat de volgende secties:  

- [Communicatie tussen site systemen in een site](#Planning_Intra-site_Com)  
  - [Site server naar distributie punt](#bkmk_site2dp)  

- [Communicatie van clients naar site systemen en-services](#Planning_Client_to_Site_System)  
  - [Communicatie tussen client en beheer punten](#bkmk_client2mp)  
  - [Communicatie van client naar distributie punt](#bkmk_client2dp)  
  - [Overwegingen voor client communicatie via internet of een niet-vertrouwd forest](#BKMK_clientspan)  

- [Communicatie tussen Active Directory forests](#Plan_Com_X-Forest)  
  - [Ondersteuning voor domein computers in een forest dat niet wordt vertrouwd door het forest van uw site server](#bkmk_noforesttrust)  
  - [Ondersteuning voor computers in een werk groep](#bkmk_workgroup)  
  - [Scenario’s voor ondersteuning van een site of hiërarchie die meerdere domeinen en forests omvat](#bkmk_span)  

## <a name="communications-between-site-systems-in-a-site"></a><a name="Planning_Intra-site_Com"></a> Communicatie tussen sitesystemen in een site  

Als Configuration Manager site systemen of-onderdelen via het netwerk met andere site systemen of-onderdelen in de site communiceren, wordt een van de volgende protocollen gebruikt, afhankelijk van hoe u de site configureert:  

- Server Message Block (SMB)  

- HTTP  

- HTTPS  

Met uitzonde ring van de communicatie van de site server naar een distributie punt, kunnen server-naar-server-communicatie op een site op elk gewenst moment plaatsvinden. Deze communicatie gebruikt geen mechanismen om de netwerk bandbreedte te beheren. Omdat u de communicatie tussen site systemen niet kunt beheren, moet u ervoor zorgen dat u site systeem servers installeert op locaties met snelle en goed verbonden netwerken.  

### <a name="site-server-to-distribution-point"></a><a name="bkmk_site2dp"></a>Site server naar distributie punt

Gebruik de volgende strategieën om u te helpen bij het beheren van de overdracht van inhoud van de site server naar distributie punten:  

- Configureer netwerkbandbreedtebeheer en -planning op het distributiepunt. Deze besturings elementen zijn vergelijkbaar met de configuraties die worden gebruikt door intersite-adressen. Gebruik deze configuratie in plaats van een andere Configuration Manager-site te installeren wanneer de overdracht van inhoud naar externe netwerk locaties uw belangrijkste bandbreedte overwegingen is.  

- U kunt een distributiepunt installeren als een voorbereid distributiepunt. Een voorbereid distributiepunt laat u inhoud gebruiken die handmatig op de distributiepuntserver wordt geplaatst en verwijdert de vereiste om inhoudsbestanden over het netwerk over te dragen.  

Zie [netwerk bandbreedte voor inhouds beheer beheren](manage-network-bandwidth.md)voor meer informatie.

## <a name="communications-from-clients-to-site-systems-and-services"></a><a name="Planning_Client_to_Site_System"></a> Communicatie van clients naar sitesystemen en services

Clients initiëren communicatie met site systeem rollen, Active Directory Domain Services en onlineservices. Om deze communicatie mogelijk te maken, moeten firewalls het netwerk verkeer tussen clients en het eind punt van hun communicatie toestaan. Zie [poorten die worden gebruikt in Configuration Manager](ports.md)voor meer informatie over de poorten en protocollen die door clients worden gebruikt wanneer ze met deze eind punten communiceren.  

Voordat een client met een site systeemrol kan communiceren, maakt de client gebruik van service locatie om een rol te vinden die het client protocol (HTTP of HTTPS) ondersteunt. Standaard gebruiken clients de meest beveiligde methode die voor hen beschikbaar is. Zie [begrijpen hoe clients site resources en-services vinden](understand-how-clients-find-site-resources-and-services.md)voor meer informatie.  

Als u HTTPS wilt gebruiken, configureert u een van de volgende opties:  

- Een open bare-sleutel infrastructuur (PKI) gebruiken en PKI-certificaten installeren op clients en servers. Zie [PKI-certificaat vereisten](../network/pki-certificate-requirements.md)voor meer informatie over het gebruik van certificaten.  

- Vanaf versie 1806 kunt u de site configureren voor het **gebruik van door Configuration Manager gegenereerde certificaten voor HTTP-site systemen**. Zie [Enhanced http](enhanced-http.md)(Engelstalig) voor meer informatie.  

Wanneer u een sitesysteemrol implementeert die gebruikmaakt van Internet Information Services (IIS) en communicatie van clients ondersteunt, moet u opgeven of clients verbinding met het sitesysteem maken via HTTP of HTTPS. Als u HTTP gebruikt, dient u ook opties voor ondertekening en versleuteling te overwegen. Zie voor meer informatie [planning voor ondertekening en versleuteling](../security/plan-for-security.md#BKMK_PlanningForSigningEncryption).  

### <a name="client-to-management-point-communication"></a><a name="bkmk_client2mp"></a>Communicatie tussen client en beheer punten

Er zijn twee fasen wanneer een client communiceert met een beheer punt: verificatie (Trans Port) en autorisatie (bericht). Dit proces varieert afhankelijk van de volgende factoren:

- Site configuratie: alleen HTTPS, staat HTTP of HTTPS toe, of staat HTTP of HTTPS toe met verbeterde HTTP ingeschakeld
- Configuratie van beheer punt: HTTPS of HTTP
- Apparaat-id voor op apparaten gerichte scenario's
- Gebruikers identiteit voor gebruikers gerichte scenario's

Gebruik de volgende tabel om te begrijpen hoe dit proces werkt:  

| Type MP  | Clientverificatie  | Client autorisatie<br>Apparaat-id  | Client autorisatie<br>Gebruikers identiteit  |
|----------|---------|---------|---------|
| HTTP     | Anoniem<br>Met verbeterde HTTP verifieert de site het token van de Azure AD- *gebruiker* of het- *apparaat* . | Locatie aanvraag: anoniem<br>Client pakket: anoniem<br>Registratie, met behulp van een van de volgende methoden om de apparaat-id te bewijzen:<br> -Anoniem (hand matige goed keuring)<br> -Geïntegreerde Windows-verificatie<br> -Azure AD- *apparaat* -token (Enhanced http)<br>Na de registratie gebruikt de client bericht ondertekening om de apparaat-id te bewijzen | Gebruik voor gebruikers gerichte scenario's een van de volgende methoden om de identiteit van de gebruiker te bewijzen:<br> -Geïntegreerde Windows-verificatie<br> -Azure AD- *gebruikers* token (Enhanced http) |
| HTTPS    | Met een van de volgende methoden:<br> -PKI-certificaat<br> -Geïntegreerde Windows-verificatie<br> -Azure AD- *gebruikers* -of- *apparaat* -token | Locatie aanvraag: anoniem<br>Client pakket: anoniem<br>Registratie, met behulp van een van de volgende methoden om de apparaat-id te bewijzen:<br> -Anoniem (hand matige goed keuring)<br> -Geïntegreerde Windows-verificatie<br> -PKI-certificaat<br> -Azure AD- *gebruikers* -of- *apparaat* -token<br>Na de registratie gebruikt de client bericht ondertekening om de apparaat-id te bewijzen | Gebruik voor gebruikers gerichte scenario's een van de volgende methoden om de identiteit van de gebruiker te bewijzen:<br> -Geïntegreerde Windows-verificatie<br> -Azure AD- *gebruikers* token |

> [!Tip]  
> Zie [beheer punt voor HTTPS inschakelen](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps)voor meer informatie over de configuratie van het beheer punt voor verschillende typen apparaat-id's en de Cloud beheer gateway.  

### <a name="client-to-distribution-point-communication"></a><a name="bkmk_client2dp"></a>Communicatie van client naar distributie punt

Wanneer een client communiceert met een distributie punt, moet deze alleen worden geverifieerd voordat de inhoud kan worden gedownload. Gebruik de volgende tabel om te begrijpen hoe dit proces werkt:

| DP-type  | Clientverificatie  |
|----------|---------|
| HTTP     | -Anoniem, indien toegestaan<br>-Geïntegreerde Windows-verificatie met computer account of netwerk toegangs account<br> -Toegangs token voor inhoud (verbeterde HTTP) |
| HTTPS    | -PKI-certificaat<br> -Geïntegreerde Windows-verificatie met computer account of netwerk toegangs account<br> -Inhouds toegangs token |

### <a name="considerations-for-client-communications-from-the-internet-or-an-untrusted-forest"></a><a name="BKMK_clientspan"></a>Overwegingen voor client communicatie via internet of een niet-vertrouwd forest

Raadpleeg voor meer informatie de volgende artikelen:

- [Een cloudbeheergateway plannen](../..//clients/manage/cmg/plan-cloud-management-gateway.md)

- [Clientbeheer via internet plannen](../../clients/manage/plan-internet-based-client-management.md)

##  <a name="communications-across-active-directory-forests"></a><a name="Plan_Com_X-Forest"></a> Communicatie tussen Active Directory-forests  

Configuration Manager ondersteunt sites en hiërarchieën die Active Directory forests omvatten. Het biedt ook ondersteuning voor domein computers die zich niet in hetzelfde Active Directory forest bevinden als de site server en computers in werk groepen.  

### <a name="support-domain-computers-in-a-forest-thats-not-trusted-by-your-site-servers-forest"></a><a name="bkmk_noforesttrust"></a>Ondersteuning voor domein computers in een forest dat niet wordt vertrouwd door het forest van uw site server

- Sitesysteemrollen in het niet-vertrouwde forest installeren met de optie om sitegegevens naar het desbetreffende Active Directory-forest te publiceren.  

- Deze computers beheren alsof ze werkgroepcomputers zijn  

Wanneer u site systeem servers in een niet-vertrouwd Active Directory forest installeert, blijft de communicatie tussen de client en de server van clients in dat forest binnen dat forest en kan Configuration Manager de computer verifiëren met behulp van Kerberos. Wanneer u site-informatie publiceert naar het forest van de client, kunnen clients profiteren van het ophalen van site-informatie, zoals een lijst met beschik bare beheer punten, van hun Active Directory-forest in plaats van deze informatie te downloaden via hun toegewezen beheer punt.  

> [!NOTE]  
> Als u apparaten wilt beheren die zich op internet bevinden, kunt u op internet gebaseerde site systeem rollen installeren in uw perimeter netwerk wanneer de site systeem servers zich in een Active Directory-forest bevinden. Dit scenario vereist geen twee richtings vertrouwensrelatie tussen het perimeter netwerk en het forest van de site server.  

### <a name="support-computers-in-a-workgroup"></a><a name="bkmk_workgroup"></a>Ondersteuning voor computers in een werk groep  

- Werkgroepcomputers handmatig goedkeuren wanneer ze HTTP-clientverbindingen met sitesysteemrollen gebruiken. Configuration Manager kunt deze computers niet verifiëren met behulp van Kerberos.  

- Werkgroepclients configureren voor het gebruik van het netwerktoegangsaccounts, zodat deze computers inhoud kunnen ophalen van distributiepunten.  

- Een alternatief mechanisme voor werkgroepclients verschaffen om beheerpunten te zoeken. Gebruik DNS-publishing, WINS of wijs rechtstreeks een beheer punt toe. Deze clients kunnen geen site-informatie ophalen van Active Directory Domain Services.  

Raadpleeg voor meer informatie de volgende artikelen:  

- [Conflicterende records beheren](../../clients/manage/manage-clients.md#BKMK_ConflictingRecords)  

- [Netwerktoegangsaccount](fundamental-concepts-for-content-management.md#accounts-used-for-content-management)  

- [Configuration Manager-clients installeren op computers in werk groepen](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)  

### <a name="scenarios-to-support-a-site-or-hierarchy-that-spans-multiple-domains-and-forests"></a><a name="bkmk_span"></a>Scenario's voor ondersteuning van een site of hiërarchie die meerdere domeinen en forests omvat  

#### <a name="scenario-1-communication-between-sites-in-a-hierarchy-that-spans-forests"></a>Scenario 1: communicatie tussen sites in een hiërarchie die forests omvat

Voor dit scenario is een twee richtings relatie tussen forests vereist die Kerberos-verificatie ondersteunt.  Als u geen twee richtings vertrouwensrelatie hebt die Kerberos-verificatie ondersteunt, biedt Configuration Manager geen ondersteuning voor een onderliggende site in het externe forest.  

Configuration Manager ondersteunt het installeren van een onderliggende site in een extern forest dat de vereiste twee richtings vertrouwensrelatie heeft met het forest van de bovenliggende site. U kunt bijvoorbeeld een secundaire site in een ander forest van de primaire bovenliggende site plaatsen, zolang de vereiste vertrouwens relatie bestaat.  

> [!NOTE]  
> Een onderliggende site kan een primaire site zijn (waarbij de centrale beheer site de bovenliggende site is) of een secundaire site.  

Intersite-communicatie in Configuration Manager maakt gebruik van database replicatie en overdrachten op basis van bestanden. Wanneer u een-site installeert, moet u een account opgeven waarmee de site op de aangewezen server moet worden geïnstalleerd. Dit account brengt ook communicatie tot stand tussen sites en onderhoudt de communicatie. Nadat de site de overdrachten op basis van bestanden en database replicatie heeft geïnstalleerd en gestart, hoeft u niets te configureren voor communicatie met de site.  

Als er sprake is van een twee richtings relatie tussen forests, hebt Configuration Manager geen aanvullende configuratie stappen nodig.  

Wanneer u een nieuwe onderliggende site installeert, configureert Configuration Manager standaard de volgende onderdelen:  

- Een intersite replicatieroute op basis van bestanden op elke site gebruikmaakt van het siteservercomputeraccount. Configuration Manager voegt het computer account van elke computer toe aan **de&lt;groep\> SMS_SiteToSiteConnection_ site** code op de doel computer.  

- Database replicatie tussen de SQL-servers op elke site.  

Stel ook de volgende configuraties in:  

- Tussenliggende firewalls en netwerk apparaten moeten de netwerk pakketten toestaan die Configuration Manager vereist.  

- Naamomzetting moet tussen de forests werken.  

- Als u een site of sitesysteemrol wilt installeren, moet u een account opgeven die lokale beheerdersmachtigingen heeft op de opgegeven computer.  

#### <a name="scenario-2-communication-in-a-site-that-spans-forests"></a>Scenario 2: communicatie in een site die forests omvat

Voor dit scenario is geen twee richtings relatie tussen forests vereist.  

Primaire sites ondersteunen de installatie van sitesysteemrollen op computers in externe forests.  

- Het Application Catalog-webservicepunt is de enige uitzondering.  Het wordt alleen ondersteund in hetzelfde forest als de site server.  

- Wanneer een site systeemrol verbindingen van het internet accepteert, installeert u als beveiligings best practice de site systeem rollen op een locatie waar de grens van het forest de site server beveiligt (bijvoorbeeld in een perimeter netwerk).  

Een sitesysteemrol installeren op een computer in een niet-vertrouwd forest:  

- Geef een **installatie account van een site systeem**op die door de site wordt gebruikt om de site systeemrol te installeren. (Dit account moet lokale beheerders referenties hebben om verbinding mee te maken.) Installeer vervolgens site systeem rollen op de opgegeven computer.  

- Selecteer de site systeem optie **de site server moet verbindingen met dit site systeem initiëren**. Voor deze instelling moet de site server verbindingen tot stand brengen met de site systeem server om gegevens over te dragen. Met deze configuratie wordt voor komen dat de computer in de niet-vertrouwde locatie contact met de site server in uw vertrouwde netwerk initieert. Voor deze verbindingen wordt het **Installatieaccount sitesysteem**gebruikt.  

Als u een sitesysteemrol gebruikt in een niet-vertrouwd forest , moeten firewalls het netwerkverkeer toestaan, zelfs wanneer de siteserver de overdracht van gegevens initieert.  

Bovendien moeten de volgende sitesysteemrollen directe toegang tot de sitedatabase hebben. Daarom moeten firewalls toepasselijk verkeer van het niet-vertrouwde forest naar de SQL Server van de site toestaan:  

- Asset Intelligence-synchronisatiepunt  

- Endpoint Protection-punt  

- Inschrijvingspunt  

- Beheerpunt  

- Reporting Service-punt  

- Statusmigratiepunt  

Zie [poorten die worden gebruikt in Configuration Manager](ports.md)voor meer informatie.  

Mogelijk moet u de toegang tot de site database configureren voor het beheer punt en het inschrijvings punt.

- Wanneer u deze rollen installeert, configureert Configuration Manager standaard het computer account van de nieuwe site systeem server als het verbindings account voor de site systeemrol. Vervolgens wordt het account toegevoegd aan de juiste SQL Server-databaserol.  

- Wanneer u deze site systeem rollen in een niet-vertrouwd domein installeert, moet u het verbindings account van de site systeemrol configureren om de site systeemrol in te scha kelen om informatie uit de data base te verkrijgen.  

Als u een domein gebruikers account configureert als verbindings account voor deze site systeem rollen, moet u ervoor zorgen dat de domein gebruikers account de juiste toegang heeft tot de SQL Server Data Base op die site:  

- Beheerpunt: **Databaseverbindingsaccount voor beheerpunt**  

- Inschrijvingspunt: **Verbindingsaccount voor inschrijvingspunt**  

Houd rekening met de volgende aanvullende informatie om sitesysteemrollen in andere forests te plannen:  

- Als u Windows Firewall uitvoert, configureert u de toepasselijke Firewall profielen om communicaties uit te voeren tussen de site database server en computers die zijn geïnstalleerd met externe site systeem rollen.

- Wanneer het beheer punt op Internet de forest vertrouwt die de gebruikers accounts bevat, wordt het gebruikers beleid ondersteund. Als er geen vertrouwensrelatie bestaat, wordt alleen computerbeleid ondersteund.  

#### <a name="scenario-3-communication-between-clients-and-site-system-roles-when-the-clients-arent-in-the-same-active-directory-forest-as-their-site-server"></a>Scenario 3: communicatie tussen clients en site systeem rollen wanneer de clients zich niet in hetzelfde Active Directory forest bevinden als hun site server

Configuration Manager ondersteunt de volgende scenario's voor clients die zich niet in hetzelfde forest bevinden als de site server van de site:  

- Er is twee richtings vertrouwensrelatie tussen de forest van de client en het forest van de site server.  

- De server van de site systeemrol bevindt zich in dezelfde forest als de client.  

- De-client bevindt zich op een domein computer die geen twee richtings vertrouwensrelatie heeft met de site server, en de site systeem rollen worden niet geïnstalleerd in het forest van de client.  

- De-client bevindt zich op een werkgroepcomputer.  

Clients op een computer die lid is van een domein kunnen Active Directory Domain Services gebruiken voor service locatie wanneer hun site wordt gepubliceerd in hun Active Directory forest.  

Site-informatie publiceren naar een andere Active Directory-forest:  

- Het forest opgeven en vervolgens publiceren naar dit forest inschakelen in het knooppunt **Active Directory-forests** van de werkruimte **Beheer** .  

- Elke site configureren om de bijbehorende gegevens te publiceren naar Active Directory-domeinservices. Deze configuratie maakt het clients in deze forest mogelijk site-informatie op te halen en beheerpunten te vinden. Voor clients die Active Directory Domain Services niet kunnen gebruiken voor service locatie, kunt u DNS, WINS of het toegewezen beheer punt van de client gebruiken.  

#### <a name="scenario-4-put-the-exchange-server-connector-in-a-remote-forest"></a><a name="bkmk_xchange"></a>Scenario 4: de Exchange Server-connector in een extern forest plaatsen  

Als u dit scenario wilt ondersteunen, moet u ervoor zorgen dat de naam omzetting tussen de forests werkt. Configureer bijvoorbeeld DNS-doorstuur servers. Wanneer u de Exchange Server-connector configureert, geeft u de intranet-FQDN van de Exchange-Server op. Zie [mobiele apparaten beheren met Configuration Manager en Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)voor meer informatie.  

## <a name="see-also"></a>Zie ook

- [De beveiliging plannen](../security/plan-for-security.md)  

- [Beveiliging en privacy voor Configuration Manager-clients](../../clients/deploy/plan/security-and-privacy-for-clients.md)  
