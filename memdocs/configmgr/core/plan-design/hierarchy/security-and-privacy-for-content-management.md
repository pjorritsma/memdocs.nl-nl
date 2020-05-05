---
title: Beveiliging en privacy voor inhouds beheer
titleSuffix: Configuration Manager
description: Optimaliseer beveiliging en privacy voor inhouds beheer in Configuration Manager.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 067922149ef268aeb6cd562816aaa4971e184fab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720854"
---
# <a name="security-and-privacy-for-content-management-in-configuration-manager"></a>Beveiliging en privacy voor inhouds beheer in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit artikel bevat beveiligings-en privacy-informatie voor inhouds beheer in Configuration Manager. 



##  <a name="security-best-practices-for-content-management"></a><a name="BKMK_Security_ContentManagement"></a>Aanbevolen beveiligings procedures voor inhouds beheer  


#### <a name="advantages-and-disadvantages-of-https-or-http-for-intranet-distribution-points"></a>Voor delen en nadelen van HTTPS of HTTP voor intranet distributie punten
Voor distributie punten op het intranet moet u rekening houden met de voor-en nadelen van het gebruik van HTTPS en HTTP. In de meeste gevallen biedt het gebruik van HTTP-en pakket toegangs accounts voor autorisatie meer beveiliging dan het gebruik van HTTPS met versleuteling, maar zonder autorisatie. Als uw inhoud echter gevoelige gegevens bevat die u tijdens de overdracht wilt versleutelen, gebruikt u HTTPS.  

-   **Wanneer u https gebruikt voor een distributie punt**, worden in Configuration Manager geen pakket toegangs accounts gebruikt om toegang tot de inhoud te verlenen, maar wordt de inhoud versleuteld wanneer deze via het netwerk wordt overgedragen.  

-   **Wanneer u http gebruikt voor een distributie punt**, kunt u pakket toegangs accounts gebruiken voor autorisatie, maar wordt de inhoud niet versleuteld wanneer deze via het netwerk wordt overgedragen.  

Met ingang van versie 1806 kunt u een **verbeterde http** inschakelen voor de site. Met deze functie kunnen clients Azure Active Directory verificatie gebruiken om veilig te communiceren met een HTTP-distributie punt. Zie [Enhanced http](enhanced-http.md)(Engelstalig) voor meer informatie.

#### <a name="protect-the-client-authentication-certificate-file"></a>Het certificaat bestand voor client verificatie beveiligen
Als u voor het distributiepunt een PKI-certificaat gebruikt voor clientverificatie in plaats van een zelfondertekend certificaat, moet u het certificaatbestand (.PFX) beschermen met een sterk wachtwoord. Als u het bestand opslaat op het netwerk, beveiligt u het netwerk kanaal wanneer u het bestand importeert in Configuration Manager.

Wanneer u een wacht woord vereist om het certificaat voor client verificatie te importeren dat het distributie punt gebruikt om te communiceren met beheer punten, helpt deze configuratie het certificaat te beschermen tegen kwaadwillende personen. Gebruik SMB-ondertekening (Server Message Block) of IPsec tussen de netwerk locatie en de site server om te voor komen dat een kwaadwillende persoon knoeit met het certificaat bestand.  

#### <a name="remove-the-distribution-point-role-from-the-site-server"></a>De distributiepuntrol van de site server verwijderen
Configuration Manager Setup installeert standaard een distributie punt op de site server. Clients hoeven niet rechtstreeks met de site server te communiceren. Als u de kwets baarheid wilt beperken, wijst u de distributiepuntrol toe aan andere site systemen en verwijdert u de rol van de site server.  

#### <a name="secure-content-at-the-package-access-level"></a>Inhoud op pakket toegangs niveau beveiligen
De distributiepunt share geeft lees toegang tot alle gebruikers. Als u wilt beperken welke gebruikers toegang hebben tot de inhoud, gebruikt u pakkettoegangsaccounts wanneer het distributiepunt is geconfigureerd voor HTTP. Deze configuratie is niet van toepassing op Cloud distributiepunten, die geen ondersteuning bieden voor pakket toegangs accounts. Zie [pakket Access accounts](accounts.md#package-access-account)voor meer informatie.

#### <a name="configure-iis-on-the-distribution-point-role"></a>IIS configureren voor de distributiepuntrol
Als Configuration Manager IIS installeert wanneer u een site systeemrol van een distributie punt toevoegt, verwijdert u HTTP-omleiding of scripts en Hulpprogram Ma's voor IIS-beheer wanneer de installatie van het distributie punt is voltooid. Het distributie punt vereist geen HTTP-omleiding of scripts en Hulpprogram Ma's voor IIS-beheer. Verwijder deze functie Services voor de webserver functie om de kwets baarheid te verminderen.  Zie [site-en site systeem vereisten](../configs/site-and-site-system-prerequisites.md)voor meer informatie over de functie Services voor de webserver functie voor distributie punten.  

#### <a name="set-package-access-permissions-when-you-create-the-package"></a>Toegangs machtigingen voor het pakket instellen wanneer u het pakket maakt
Omdat wijzigingen in de toegangs accounts van de pakket bestanden alleen van kracht worden wanneer u het pakket opnieuw distribueert, stelt u de toegangs machtigingen voor het pakket zorgvuldig in wanneer u het pakket voor het eerst maakt. Deze configuratie is belang rijk wanneer het pakket groot is of wordt gedistribueerd naar een groot aantal distributie punten en wanneer de netwerk bandbreedte capaciteit voor inhouds distributie beperkt is.  

#### <a name="implement-access-controls-to-protect-media-that-contains-prestaged-content"></a>Implementeer toegangs beheer om media te beveiligen die voor bereide inhoud bevatten
Voor bereide inhoud is gecomprimeerd, maar niet versleuteld. Een aanvaller kan de bestanden die worden gedownload naar apparaten lezen en wijzigen. Configuration Manager-clients inhoud afwijzen waarmee is geknoeid, maar deze worden nog steeds gedownload.  

#### <a name="import-prestaged-content-with-extractcontent"></a>Voor bereide inhoud importeren met extract content
Importeer voor bereide inhoud alleen met behulp van het opdracht regel programma Extract content. exe. Gebruik alleen het geautoriseerde opdracht regel programma dat wordt meegeleverd met Configuration Manager om knoeien en uitbrei ding van bevoegdheden te voor komen.  

#### <a name="secure-the-communication-channel-between-the-site-server-and-the-package-source-location"></a>Het communicatie kanaal tussen de site server en de bron locatie van het pakket beveiligen
Gebruik IPsec of SMB-ondertekening tussen de site server en de bron locatie van het pakket wanneer u toepassingen en pakketten maakt. Deze configuratie helpt te voor komen dat een kwaadwillende persoon knoeit met de bron bestanden.  

#### <a name="remove-default-virtual-directories-for-custom-website-with-the-distribution-point-role"></a>Standaard virtuele mappen voor aangepaste website verwijderen met de distributiepunt rol
Als u de site configuratie optie wijzigt om een aangepaste website te gebruiken in plaats van de standaard website na het installeren van een distributie punt, verwijdert u de virtuele standaard mappen. Wanneer u overschakelt van de standaard website naar een aangepaste website, Configuration Manager verwijdert de oude virtuele mappen niet. Verwijder de volgende virtuele mappen die Configuration Manager oorspronkelijk is gemaakt op de standaard website:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  


#### <a name="for-cloud-distribution-points-protect-your-azure-subscription-details-and-certificates"></a>Beveilig uw Azure-abonnements gegevens en-certificaten voor Cloud distributiepunten
Wanneer u Cloud distributiepunten gebruikt, moet u de volgende items met hoge waarde beveiligen:
- De gebruikers naam en het wacht woord voor uw Azure-abonnement
- Het Azure-beheer certificaat 
- Het service certificaat van het Cloud distributiepunt

Sla de certificaten veilig op. Gebruik IPsec of SMB-ondertekening tussen de site systeem server en de bron locatie als u het distributie punt van de Cloud via het netwerk naar de andere gebruikers bladert.  

#### <a name="for-service-continuity-monitor-the-expiry-date-of-the-cloud-distribution-point-certificates"></a>Bewaak de verval datum van de certificaten van het Cloud distributiepunt voor de continuïteit van de service.
Configuration Manager waarschuwt u niet wanneer de geïmporteerde certificaten voor het Cloud distributiepunt op het punt staan te verlopen. De verval datums onafhankelijk van Configuration Manager bewaken. Zorg ervoor dat u de nieuwe certificaten vernieuwt en vervolgens importeert voor de verval datum. Deze actie is belang rijk als u een server verificatie certificaat van een externe, open bare provider aanschaft, omdat u mogelijk extra tijd nodig hebt om een vernieuwend certificaat te verkrijgen.  

 Als een van beide certificaten verloopt, genereert Cloud Services Manager de status bericht-ID **9425**. Het bestand CloudMgr. log bevat een vermelding om aan te geven dat de **status van het certificaat verlopen is**, waarbij de verval datum ook wordt geregistreerd in UTC.  



## <a name="security-considerations-for-content-management"></a>Beveiligingsoverwegingen voor inhoudsbeheer  

Houd rekening met de volgende punten bij het plannen van inhouds beheer:  

-   Clients valideren inhoud pas nadat deze is gedownload.  

     Configuration Manager-clients valideren de hash van inhoud pas nadat deze is gedownload naar de client cache. Als een kwaadwillende persoon knoeit met de lijst met bestanden die moeten worden gedownload of met de inhoud zelf, kan het download proces aanzienlijke netwerk bandbreedte in beslag nemen, maar alleen voor de client om vervolgens de inhoud te verwijderen wanneer de ongeldige hash wordt aangetroffen.  

-   Wanneer u Cloud distributiepunten gebruikt, wordt de toegang tot de inhoud automatisch beperkt tot uw onderneming. U kunt deze niet verder beperken tot geselecteerde gebruikers of groepen.  

-   Wanneer u Cloud distributiepunten gebruikt, worden clients door het beheer punt geverifieerd en wordt vervolgens een Configuration Manager token gebruikt voor toegang tot Cloud distributiepunten. Het token is acht uur geldig. Dit gedrag betekent dat als u een client blokkeert omdat deze niet meer wordt vertrouwd, de inhoud van een Cloud distributiepunt kan blijven downloaden totdat de geldigheids periode van dit token is verlopen. Op dit moment uitgeven het beheer punt geen ander token voor de client, omdat de client is geblokkeerd.  

     Als u wilt voor komen dat een geblokkeerde client inhoud in dit acht uur kan downloaden, stopt u de Cloud service. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **Cloud distributiepunten** .  



##  <a name="privacy-information-for-content-management"></a><a name="BKMK_Privacy_ContentManagement"></a> Informatie over privacy voor inhoudsbeheer  

 Configuration Manager bevat geen gebruikers gegevens in inhouds bestanden, hoewel een gebruiker met beheerders rechten kan kiezen om deze actie uit te voeren.  



## <a name="see-also"></a>Zie ook

- [Basisconcepten voor inhoudsbeheer](fundamental-concepts-for-content-management.md)  

- [Beveiliging en privacy voor toepassings beheer](../../../apps/plan-design/security-and-privacy-for-application-management.md)  

- [Beveiliging en privacy voor software-updates](../../../sum/plan-design/security-and-privacy-for-software-updates.md)  

- [Beveiliging en privacy voor besturingssysteemimplementatie](../../../osd/plan-design/security-and-privacy-for-operating-system-deployment.md)  
