---
title: Clientbeheer via internet
titleSuffix: Configuration Manager
description: Maak een plan voor het beheren van op internet gebaseerde clients in Configuration Manager.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f7054c75643c6ffa37decba74f9fe85831728985
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587217"
---
# <a name="plan-for-internet-based-client-management-in-configuration-manager"></a>Plannen voor client beheer op internet in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik client beheer op internet (IBCM) om Configuration Manager-clients te beheren wanneer ze niet zijn verbonden met uw interne netwerk. Voor delen van het gebruik van IBCM:

- Volledig beheer van servers en rollen die de service bieden
- Geen Cloud service afhankelijkheid
- Er is mogelijk geen virtueel particulier netwerk (VPN) vereist
- Alle kosten zijn gekoppeld aan de on-premises service

Vanwege de hogere beveiligings vereisten voor het beheren van client computers op een openbaar netwerk, is voor IBCM het gebruik van PKI-certificaten vereist. Deze configuratie zorgt ervoor dat de verbindingen worden geverifieerd door een onafhankelijke instantie. Wanneer IBCM-clients en site servers gegevens verzenden, worden deze versleuteld en beveiligd.  

## <a name="client-communications"></a>Communicatie met de client

De volgende site systeem rollen op primaire sites ondersteunen verbindingen van clients die zich op niet-vertrouwde locaties bevinden:

> [!NOTE]
> Hoewel IBCM voornamelijk gericht is op het scenario op internet, is hetzelfde gedrag van toepassing op clients in een niet-vertrouwde Active Directory forest. Secundaire sites ondersteunen geen client verbindingen van niet-vertrouwde locaties.

- Certificaat registratiepunt voor de Configuration Manager-beleids module (NDES)

- Distributiepunt

- Cloud-gebaseerd distributiepunt

- Proxypunt voor inschrijving

- Terugvalstatuspunt

- Beheerpunt

- Software-updatepunt

> [!NOTE]
> De ondersteuning voor de functies van de toepassings catalogus is beëindigd met versie 1910. Zie [de Application Catalog verwijderen](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat)voor meer informatie. Voor Configuration Manager versies 1906 en eerder die nog steeds worden ondersteund, kan het Application catalog-website punt verbindingen van clients op Internet accepteren.

### <a name="about-internet-facing-site-systems"></a>Over Internet gerichte site systemen

Er is geen vertrouwens relatie tussen het forest van de client en de site systeem server. Wanneer het forest dat een Internet gericht site systeem bevat, echter het forest met de gebruikers accounts vertrouwt, ondersteunt deze configuratie gebruikers beleid voor apparaten op Internet wanneer u de client instelling **client beleid** **gebruikers beleids aanvragen van internetclients inschakelen**.

De volgende configuraties illustreren bijvoorbeeld wanneer IBCM gebruikers beleid voor apparaten op internet ondersteunt:

- Het beheer punt op Internet bevindt zich in het perimeter netwerk. Dat netwerk heeft ook een alleen-lezen domein controller om de gebruiker te verifiëren. Een firewall tussen de perimeter netwerk en interne netwerken staat Active Directory-pakketten toe.

- Het gebruikers account bevindt zich in het forest op het intranet. Het beheer punt op Internet bevindt zich in het perimeter forest. De perimeter forest vertrouwt het interne forest. Een firewall tussen de perimeter netwerk en interne netwerken staat de verificatie pakketten toe.

- Het gebruikers account en het internet-gebaseerd beheer punt bevinden zich beide in de intranet-forest. U publiceert het beheer punt op internet met een webproxyserver.

### <a name="use-a-web-proxy-server"></a>Een webproxyserver gebruiken

U kunt op internet gebaseerde site systemen op het intranet plaatsen wanneer u ze op internet publiceert met een webproxyserver. Deze site systemen alleen configureren voor client verbindingen vanaf internet of client verbindingen van Internet en intranet. Wanneer u een webproxyserver gebruikt, kunt u deze configureren voor Secure Sockets Layer (SSL) bridging voor SSL-of SSL-Tunneling.

#### <a name="ssl-bridging-to-ssl"></a>SSL-bridging naar SSL

SSL-bridging naar SSL is de aanbevolen en veiligere configuratie, omdat deze gebruikmaakt van SSL-beëindiging met verificatie. Client computers worden geverifieerd met computer verificatie. Mobiele apparaten die u inschrijft met Configuration Manager bieden geen ondersteuning voor SSL-bridging.

Met SSL-beëindiging bij de proxy inspecteert het pakketten van het internet voordat deze naar het interne netwerk worden doorgestuurd. De proxy verifieert de verbinding van de client, beëindigt deze en opent vervolgens een nieuwe geverifieerde verbinding met de site systemen op internet. Wanneer Configuration Manager-clients een proxy gebruiken, bevat de-client veilig zijn identiteit (GUID) in de pakket lading. Het beheer punt beschouwt de proxy niet als de client. Configuration Manager biedt geen ondersteuning voor bridging met HTTP naar HTTPS of van HTTPS naar HTTP.

> [!NOTE]
> Configuration Manager biedt geen ondersteuning voor het instellen van SSL-bridging configuraties van derden. Bijvoorbeeld Citrix NetScaler of F5 BIG-IP. Neem contact op met de leverancier van uw apparaat om deze te configureren voor gebruik met Configuration Manager.

#### <a name="tunneling"></a>Tunneling

Als uw proxy webserver de vereisten voor SSL-bridging niet kan ondersteunen, ondersteunt Configuration Manager ook SSL-Tunneling. U kunt ook SSL-Tunneling gebruiken ter ondersteuning van mobiele apparaten die u registreert met Configuration Manager. Het is een minder veilige optie omdat de proxy de SSL-pakketten van het internet naar de site systemen stuurt zonder SSL-beëindiging. De-proxy inspecteert de pakketten niet op schadelijke inhoud. Als u SSL-tunneling gebruikt, zijn er geen certificaatvereisten voor de proxywebserver.

## <a name="plan-for-internet-based-clients"></a>Plannen voor clients op Internet

Bepaal of u uw op internet gebaseerde clients wilt configureren voor beheer op het intranet en het Internet, of alleen voor client beheer op internet. U kunt deze beheer optie alleen configureren tijdens de client installatie. Installeer de-client opnieuw om deze later te wijzigen.

> [!NOTE]
> Als u een beheer punt configureert voor de ondersteuning van Internet-clients, worden clients die verbinding maken met dit beheer punt, Internet ondersteund wanneer ze de lijst met beschik bare beheer punten vernieuwen.
>
> U hoeft de configuratie van client beheer alleen via internet niet te beperken tot internet. U kunt deze ook op het intranet gebruiken.

Clients die u configureert voor alleen-Internet beheer communiceren alleen met de site systemen die u configureert voor client verbindingen vanaf internet. Gebruik deze configuratie in de volgende scenario's:

- Voor computers waarvan u weet dat ze nooit verbinding maken met uw intranet. Bijvoorbeeld Point of sale-computers op externe locaties.
- Client communicatie beperken tot alleen HTTPS. Bijvoorbeeld om firewall-en beperkt beveiligings beleid te ondersteunen.
- Wanneer u site systemen op Internet installeert in een perimeter netwerk en u deze servers als Configuration Manager-clients wilt beheren.

> [!NOTE]
> Als u werkgroepcomputers op internet wilt beheren, installeert u ze als alleen Internet.
>
> Wanneer u een mobiel apparaat configureert om een beheer punt op internet te gebruiken, wordt dit automatisch geconfigureerd als alleen Internet.

U kunt andere clients configureren voor client beheer op internet en intranet. Wanneer ze een netwerk wijziging detecteren, scha kelen ze automatisch tussen IBCM en intranet-client beheer. Als deze clients een beheer punt kunnen vinden en er verbinding mee maken dat client verbindingen op het intranet ondersteunt, worden deze clients beheerd als intranet-clients. Intranet-clients beschikken over de volledige functionaliteit van Configuration Manager. Als de clients geen beheer punt kunnen vinden of er verbinding mee kan maken die client verbindingen op het intranet ondersteunt, proberen ze verbinding te maken met een beheer punt op internet. Als deze actie slaagt, worden deze clients vervolgens beheerd door de site systemen op internet in hun toegewezen site.

Het voor deel van automatische switching is dat clients alle functies kunnen gebruiken wanneer ze verbinding maken met het intranet en essentiële beheer ontvangen wanneer ze op het Internet zijn. Het downloaden van inhoud dat wordt gestart op internet kan naadloos worden hervat op het intranet en op de andere manier.

## <a name="prerequisites"></a>Vereisten

IBCM in Configuration Manager heeft de volgende afhankelijkheden:

- Clients hebben een Internet verbinding nodig. Configuration Manager maakt gebruik van de bestaande Internet verbinding van het apparaat. Mobiele apparaten moeten een rechtstreekse Internet verbinding hebben. Volledige client computers kunnen een rechtstreekse Internet verbinding hebben of verbinding maken met behulp van een proxy server.

- Site systemen die ondersteuning bieden voor IBCM, moeten een Internet verbinding hebben en moeten zich in een Active Directory domein benemen. De site systemen op internet hebben geen vertrouwens relatie nodig met het Active Directory forest van de site server. Wanneer het beheer punt op internet echter de gebruiker kan verifiëren met behulp van Windows-verificatie, wordt het gebruikers beleid ondersteund. Als Windows-verificatie mislukt, wordt alleen het beleid voor apparaten ondersteund.

    > [!NOTE]
    > Om gebruikers beleid te ondersteunen, moet u ook de volgende client instellingen inschakelen in de **client beleids** groep:
    >
    > - **Polling voor gebruikersbeleid inschakelen op clients**
    > - **Gebruikersbeleidsaanvragen van internetclients inschakelen**  

- Een open bare-sleutel infrastructuur (PKI) voor het implementeren en beheren van de vereiste certificaten voor op internet gebaseerde clients en site systeem servers. Zie [PKI-certificaat vereisten](../../plan-design/network/pki-certificate-requirements.md)voor meer informatie.

- Registreer open bare DNS-host-vermeldingen voor de Internet FQDN-namen (FULLy Qualified Domain names) van site systemen die IBCM ondersteunen.

### <a name="client-communication-requirements"></a>Client communicatie vereisten

Tussenliggende firewalls of proxy servers moeten client communicatie toestaan voor site systemen op Internet:

- Ondersteuning voor HTTP 1.1  

- Sta HTTP-inhoudstype van meerdelige MIME-bijlage toe (meerdelig/gemengd en toepassing/octet-stream)  

#### <a name="verbs"></a>Termen

Sta de volgende bewerkingen toe voor de site systeem Server functies op Internet:

| Rol | Termen |
|------|-------|
| Beheerpunt | -HEAD<br>-CCM_POST<br>-BITS_POST<br>- GET<br>-PROPFIND |
| Distributiepunt | -HEAD<br>- GET<br>-PROPFIND |
| Terugvalstatuspunt | POST |
| Application catalog-website punt | -POST<br>-GET |

#### <a name="http-headers"></a>HTTP-headers

Sta de volgende HTTP-headers toe voor de site systeem Server rollen op Internet:

| Rol | HTTP-headers |
|------|--------------|
| Beheerpunt | Bereik<br>- CCMClientID:<br>- CCMClientIDSignature:<br>- CCMClientTimestamp:<br>- CCMClientTimestampsSignature: |
| Distributiepunt | Bereik: |

Zie de documentatie voor Windows Server Update Services (WSUS) voor vergelijk bare communicatie vereisten wanneer u het software-update punt voor client verbindingen van het Internet gebruikt.

## <a name="unsupported-features"></a>Niet-ondersteunde functies

Niet alle client beheer functionaliteit is geschikt voor Internet. Configuration Manager biedt geen ondersteuning voor sommige functies voor clients op internet. Deze niet-ondersteunde functies vertrouwen doorgaans op Active Directory Domain Services of zijn niet geschikt voor een openbaar netwerk.

De volgende functies worden niet ondersteund wanneer u clients op internet beheert met IBCM:

- Client implementatie via internet, zoals client push en client implementatie op basis van software-updates. Hand matige client installatie gebruiken.

- Automatische sitetoewijzing

- Wake-on-LAN

- Implementatie van besturings systeem. U kunt echter taken reeksen implementeren die geen besturings systeem implementeren.

- Extern beheer

- Software-implementatie voor gebruikers. Deze functie is afhankelijk van de toepassings catalogus, die is afgeschaft.

- Zwervende clients. Roaming maakt het clients mogelijk altijd de dichtstbijzijnde distributiepunten te vinden om inhoud te downloaden. Clients niet-deterministisch selecteren een van de site systemen op internet, ongeacht de band breedte of fysieke locatie.

Wanneer u een software-update punt configureert om verbindingen van het Internet te accepteren, moeten clients op Internet altijd scannen op basis van dit software-update punt om te bepalen welke software-updates vereist zijn. Wanneer deze clients zich op het Internet bevinden, proberen ze eerst de software-updates te downloaden van Microsoft Update in plaats van vanaf een distributie punt op internet. Als dit gedrag mislukt, zullen ze proberen de vereiste software-updates te downloaden vanaf een op internet gebaseerd distributie punt.

> [!TIP]
> De Configuration Manager-client bepaalt automatisch of deze zich op het intranet of Internet bevindt. Als de client verbinding kan maken met een domein controller of een on-premises beheer punt, wordt het verbindings type ingesteld op ' momenteel *intranet*'. Anders wordt overgeschakeld naar ' momenteel *Internet*' en communiceert deze met de site systemen die aan de site zijn toegewezen.
