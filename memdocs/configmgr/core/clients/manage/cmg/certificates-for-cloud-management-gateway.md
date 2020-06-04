---
title: Certificaten CMG
titleSuffix: Configuration Manager
description: Meer informatie over de verschillende digitale certificaten die u kunt gebruiken met de Cloud beheer gateway.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: 7e9602ef5ea784dd3e97578d5ff585f2ca662c1e
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347199"
---
# <a name="certificates-for-the-cloud-management-gateway"></a>Certificaten voor de Cloud beheer gateway

*Van toepassing op: Configuration Manager (huidige vertakking)*

Afhankelijk van het scenario dat u gebruikt voor het beheren van clients op internet met de Cloud Management Gateway (CMG), hebt u een of meer van de volgende digitale certificaten nodig:  

- [Certificaat voor CMG-Server verificatie](#bkmk_serverauth)  
  - [Vertrouwde basis certificaat CMG naar clients](#bkmk_cmgroot)  
  - [Certificaat voor Server verificatie dat is uitgegeven door de open bare provider](#bkmk_serverauthpublic)  
  - [Server verificatie certificaat dat is uitgegeven door Enter prise PKI](#bkmk_serverauthpki)  

- [Clientverificatiecertificaat](#bkmk_clientauth)  
  - [Door client vertrouwd basis certificaat naar CMG](#bkmk_clientroot)  

- [Beheer punt voor HTTPS inschakelen](#bkmk_mphttps)  

- [Azure-beheer certificaat](#bkmk_azuremgmt)  

Zie voor meer informatie over de verschillende scenario's [plannen voor Cloud beheer gateway](plan-cloud-management-gateway.md).

## <a name="general-information"></a>Algemene informatie

<!--SCCMDocs issue #779-->
Certificaten voor de Cloud beheer gateway ondersteunen de volgende configuraties:  

- 2048-bits of 4096-bits sleutel lengte

- Belangrijkste opslag providers voor persoonlijke sleutels van certificaten. Zie voor meer informatie [overzicht CNG-certificaten](../../../plan-design/network/cng-certificates-overview.md).  

- Wanneer u Windows configureert met het volgende beleid: **systeem cryptografie: gebruik FIPS-compatibele algoritmen voor versleuteling, hashing en ondertekening**  

- **TLS 1,2**. Zie [TLS 1,2 inschakelen](../../../plan-design/security/enable-tls-1-2.md)voor meer informatie.  

## <a name="cmg-server-authentication-certificate"></a><a name="bkmk_serverauth"></a>Certificaat voor CMG-Server verificatie

*Dit certificaat is vereist in alle scenario's.*

U geeft dit certificaat op wanneer u de CMG maakt in de Configuration Manager-console.

De CMG maakt een HTTPS-service waarmee op internet gebaseerde clients verbinding maken. De server vereist een server verificatie certificaat om het beveiligde kanaal te bouwen. Haal een certificaat voor dit doel op bij een open bare provider of geef het op uit uw open bare-sleutel infrastructuur (PKI). Zie [CMG voor vertrouwde basis certificaten voor clients](#bkmk_cmgroot)voor meer informatie.

> [!NOTE]
> Het certificaat voor CMG-Server verificatie ondersteunt joker tekens. Sommige certificerings instanties geven certificaten uit met behulp van een Joker teken voor de hostnaam. Bijvoorbeeld `*.contoso.com`. Sommige organisaties gebruiken Joker certificaten om hun PKI te vereenvoudigen en de onderhouds kosten te verlagen.<!--491233-->  
>
> Zie [een CMG instellen](setup-cloud-management-gateway.md#set-up-a-cmg)voor meer informatie over het gebruik van een certificaat met Joker tekens met een CMG.<!--SCCMDocs issue #565-->  

Dit certificaat vereist een wereld wijd unieke naam voor het identificeren van de service in Azure. Voordat u een certificaat aanvraagt, controleert u of de Azure-domein naam die u wilt, uniek is. Bijvoorbeeld *GraniteFalls.CloudApp.net*.

1. Meld u aan bij de [Azure-portal](https://portal.azure.com).
1. Selecteer **alle resources**en selecteer vervolgens **toevoegen**.
1. Zoek naar de **Cloud service**. Selecteer **Maken**.
1. Typ in het veld **DNS-naam** het gewenste voor voegsel, bijvoorbeeld *GraniteFalls*. De interface geeft aan of de domein naam beschikbaar is of al door een andere service wordt gebruikt.

    > [!Important]  
    > Maak de service niet in de portal. Gebruik dit proces alleen om de beschik baarheid van de naam te controleren.

Als u ook de CMG voor inhoud wilt inschakelen, controleert u of de naam van de CMG-service ook een unieke naam voor een Azure-opslag account is. Als de naam van de Cloud service CMG uniek is, maar de naam van het opslag account niet, kan Configuration Manager de service niet inrichten in Azure. Herhaal het bovenstaande proces in de Azure Portal met de volgende wijzigingen:

- Zoeken naar **opslag account**
- Test uw naam in het veld **naam van opslag account**

Het voor voegsel van de DNS-naam, bijvoorbeeld *GraniteFalls*, moet 3 tot 24 tekens lang zijn en mag alleen alfanumerieke tekens gebruiken. Gebruik geen speciale tekens, zoals een streepje ( `-` ).<!-- SCCMDocs#1080 -->

### <a name="cmg-trusted-root-certificate-to-clients"></a><a name="bkmk_cmgroot"></a>Vertrouwde basis certificaat CMG naar clients

Clients moeten het certificaat voor CMG-Server verificatie vertrouwen. Er zijn twee methoden om deze vertrouwens relatie uit te voeren:

- Gebruik een certificaat van een open bare en wereld wijd vertrouwde certificaat provider. Bijvoorbeeld, maar niet beperkt tot, DigiCert, Thawte of VeriSign. Windows-clients bevatten vertrouwde basis certificerings instanties (Ca's) van deze providers. Door gebruik te maken van een server verificatie certificaat dat is uitgegeven door een van deze providers, vertrouwen uw clients het automatisch.  

- Gebruik een certificaat dat is uitgegeven door een CA voor ondernemingen vanuit uw open bare-sleutel infrastructuur (PKI). De meeste Enter prise PKI-implementaties voegen de vertrouwde basis certificerings instanties toe aan Windows-clients. U kunt bijvoorbeeld Active Directory Certificate Services gebruiken met groeps beleid. Als u het certificaat voor verificatie van de CMG-server uitgeeft van een CA die niet automatisch wordt vertrouwd door uw clients, voegt u het vertrouwde basis certificaat van de certificerings instantie toe aan clients op internet.  

  - U kunt ook Configuration Manager-certificaat profielen gebruiken om certificaten in te richten op clients. Zie [Inleiding tot certificaat profielen](../../../../protect/deploy-use/introduction-to-certificate-profiles.md)voor meer informatie.

  - Als u van plan bent om [de Configuration Manager-client te installeren vanuit intune](../../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client), kunt u ook intune-certificaat profielen gebruiken om certificaten in te richten op clients. Zie [Configure a Certificate profile](https://docs.microsoft.com/intune/certificates-configure)(Engelstalig) voor meer informatie.

### <a name="server-authentication-certificate-issued-by-public-provider"></a><a name="bkmk_serverauthpublic"></a>Certificaat voor Server verificatie dat is uitgegeven door de open bare provider

Een certificaat provider van derden kan geen certificaat voor CloudApp.net maken, aangezien dat domein eigendom is van micro soft. U kunt alleen een certificaat ophalen dat is uitgegeven voor een domein dat u bezit. De belangrijkste reden voor het verkrijgen van een certificaat van een externe provider is dat uw klanten het basis certificaat van de provider al vertrouwen.

Gebruik het volgende proces om een DNS-alias te maken:

1. Maak een canonieke naam record (CNAME) in de open bare DNS van uw organisatie. Met deze record wordt een alias voor de CMG gemaakt met een beschrijvende naam die u in het open bare certificaat gebruikt.

    Bijvoorbeeld, contoso noemt hun CMG **GraniteFalls**. Deze naam wordt **GraniteFalls.CloudApp.net** in Azure. In de open bare DNS-naam ruimte van Contoso maakt de DNS-beheerder een nieuwe CNAME-record voor **GraniteFalls.contoso.com** voor de werkelijke hostnaam, **GraniteFalls.CloudApp.net**.  

2. Een certificaat voor Server verificatie aanvragen bij een open bare provider met behulp van de algemene naam (CN) van de CNAME-alias.
Contoso gebruikt bijvoorbeeld **GraniteFalls.contoso.com** voor het certificaat cn.  

3. Maak de CMG in de Configuration Manager-console met behulp van dit certificaat. Op de pagina **instellingen** van de Wizard Create cloudbeheergateway:  

    - Wanneer u het server certificaat voor deze Cloud service toevoegt (uit het **certificaat bestand**), haalt de wizard de hostnaam uit de certificaat-CN op als de service naam.  

    - Vervolgens wordt die hostnaam toegevoegd aan **cloudapp.net**of **Usgovcloudapp.net** voor de Azure US Government-Cloud, als de service-FQDN voor het maken van de service in Azure.  

    - Wanneer contoso bijvoorbeeld de CMG maakt, haalt Configuration Manager de hostnaam **GraniteFalls** uit de certificaat-cn. Azure maakt de daad werkelijke service als **GraniteFalls.CloudApp.net**.  

Wanneer u het CMG-exemplaar maakt in Configuration Manager, terwijl het certificaat GraniteFalls.Contoso.com heeft Configuration Manager, haalt alleen de hostnaam op, bijvoorbeeld: GraniteFalls. Deze hostnaam wordt toegevoegd aan CloudApp.net, die door Azure is vereist bij het maken van een Cloud service. De CNAME-alias in de DNS-naam ruimte voor uw domein, Contoso.com, wijst deze twee FQDN-namen samen. Configuration Manager geeft clients een beleid voor toegang tot deze CMG, de DNS-toewijzing verbindt het samen zodat ze veilig toegang hebben tot de service in Azure.<!--SCCMDocs issue #565-->  

### <a name="server-authentication-certificate-issued-from-enterprise-pki"></a><a name="bkmk_serverauthpki"></a>Server verificatie certificaat dat is uitgegeven door Enter prise PKI

Maak een aangepast SSL-certificaat voor de CMG op dezelfde wijze als voor een Cloud distributiepunt. Volg de instructies voor [het implementeren van het service certificaat voor distributie punten in de Cloud,](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012) maar u moet de volgende dingen doen:

- Geef bij het aanvragen van het aangepaste webserver certificaat een FQDN op voor de algemene naam van het certificaat. Deze naam kan een open bare domein naam zijn waarvan u de eigenaar bent, of u kunt het cloudapp.net-domein gebruiken. Als u uw eigen open bare domein gebruikt, raadpleegt u het bovenstaande proces voor het maken van een DNS-alias in de open bare DNS-server van uw organisatie.  

- Wanneer u het open bare domein cloudapp.net gebruikt voor het CMG-webserver certificaat:  

  - Gebruik in de open bare Azure-Cloud een naam die eindigt op **cloudapp.net**  

  - Een naam gebruiken die eindigt op **usgovcloudapp.net** voor de Azure-Cloud voor de Amerikaanse overheid  

## <a name="client-authentication-certificate"></a><a name="bkmk_clientauth"></a>Certificaat voor client verificatie

*Dit certificaat is vereist voor Internet-clients met Windows 8,1 en Windows 10-apparaten die geen deel uitmaken van Azure Active Directory (Azure AD). Het is ook vereist op het CMG-verbindings punt. Het is niet vereist voor Windows 10-clients die lid zijn van Azure AD.*

De clients gebruiken dit certificaat om te verifiëren bij de CMG. Voor Windows 10-apparaten die lid zijn van hybride of het Cloud domein, is dit certificaat niet vereist omdat ze Azure AD gebruiken voor verificatie.

Richt dit certificaat in buiten de context van Configuration Manager. Gebruik bijvoorbeeld Active Directory Certificate Services en groeps beleid om certificaten voor client verificatie uit te geven. Zie [het client certificaat voor Windows-computers implementeren](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)voor meer informatie.

Voor het veilig door sturen van client aanvragen vereist het CMG-verbindings punt een certificaat voor client verificatie dat overeenkomt met het Server verificatie certificaat op het HTTPS-beheer punt. Als clients gebruikmaken van Azure AD-verificatie, of als u het beheer punt voor verbeterde HTTP configureert, is dit certificaat niet vereist. Zie [beheer punt voor HTTPS inschakelen](#bkmk_mphttps)voor meer informatie.

> [!NOTE]
> Micro soft raadt aan om apparaten te koppelen aan Azure AD. Op internet gebaseerde apparaten kunnen Azure AD gebruiken om te verifiëren met Configuration Manager. Het schakelt ook zowel apparaat-als gebruikers scenario's in, ongeacht of het apparaat op internet is of is verbonden met het interne netwerk. Zie [de client installeren en registreren met Azure AD Identity](../../deploy/deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity)voor meer informatie.
>
> Vanaf versie 2002,<!--5686290--> Configuration Manager breidt de ondersteuning uit voor apparaten op Internet die niet vaak verbinding maken met het interne netwerk, geen lid kunnen worden van Azure Active Directory (Azure AD) en geen methode hebben om een door PKI uitgegeven certificaat te installeren. Zie [verificatie op basis van tokens voor CMG](../../deploy/deploy-clients-cmg-token.md)voor meer informatie.

### <a name="client-trusted-root-certificate-to-cmg"></a><a name="bkmk_clientroot"></a>Door client vertrouwd basis certificaat naar CMG

*Dit certificaat is vereist voor het gebruik van certificaten voor client verificatie. Wanneer alle clients Azure AD gebruiken voor verificatie, is dit certificaat niet vereist.*

U geeft dit certificaat op wanneer u de CMG maakt in de Configuration Manager-console.

De CMG moet de client authenticatie certificaten vertrouwen. Geef de vertrouwde basis certificaat keten op om deze vertrouwens relatie uit te voeren. Zorg ervoor dat alle certificaten in de vertrouwens keten zijn toegevoegd. Als het client verificatie certificaat bijvoorbeeld wordt uitgegeven door een tussenliggende certificerings instantie, moet u zowel de tussenliggende als de basis-CA-certificaten toevoegen.

> [!Note]  
> Wanneer u een CMG maakt, hoeft u niet langer een vertrouwd basis certificaat op te geven op de pagina instellingen. Dit certificaat is niet vereist wanneer u Azure Active Directory (Azure AD) gebruikt voor client verificatie, maar dat in de wizard vereist is. Als u certificaten voor PKI-client verificatie gebruikt, moet u nog steeds een vertrouwd basis certificaat toevoegen aan de CMG.<!--SCCMDocs-pr issue #2872 SCCMDocs issue #1319-->
>
> In versie 1902 en eerder kunt u slechts twee vertrouwde basis certificerings instanties en vier tussenliggende (onderliggende) Ca's toevoegen.

#### <a name="export-the-client-certificates-trusted-root"></a>De vertrouwde basis van het client certificaat exporteren

Nadat u een certificaat voor client verificatie hebt verleend aan een computer, gebruikt u dit proces op die computer om het vertrouwde basis bestand te exporteren.

1. Open het menu Start. Typ ' uitvoeren ' om het venster uitvoeren te openen. Open `mmc`.  

2. Kies in het menu bestand de optie **module toevoegen/verwijderen...**.  

3. Selecteer in het dialoog venster modules toevoegen of verwijderen de optie **certificaten**en selecteer vervolgens **toevoegen**.  

    1. Selecteer **computer account**in het dialoog venster certificaten module en selecteer vervolgens **volgende**.  

    1. Selecteer in het dialoog venster computer selecteren de optie **lokale computer**en selecteer vervolgens **volt ooien**.  

    1. Selecteer **OK**in het dialoog venster modules toevoegen of verwijderen.  

4. Vouw **certificaten**uit, vouw **persoonlijk**uit en selecteer **certificaten**.  

5. Selecteer een certificaat waarvan het beoogde doel is **client verificatie**.  

    1. Selecteer in het menu actie **openen**.  

    1. Ga naar het tabblad **certificeringspad** .  

    1. Selecteer het volgende certificaat in de keten en selecteer **certificaat weer geven**.  

6. In het dialoog venster Nieuw certificaat gaat u naar het tabblad **Details** . Selecteer **kopiëren naar bestand...**.  

7. Voltooi de wizard Certificaat exporteren met de standaard indeling voor het certificaat, **der Encoded Binary X. 509 (. CER)**. Noteer de naam en locatie van het geëxporteerde certificaat.  

8. Exporteer alle certificaten in het certificeringspad van het oorspronkelijke certificaat voor client verificatie. Denk na over welke geëxporteerde certificaten tussenliggende Ca's zijn en welke vertrouwde basis certificerings instanties zijn.  

## <a name="enable-management-point-for-https"></a><a name="bkmk_mphttps"></a>Beheer punt voor HTTPS inschakelen

Richt dit certificaat in buiten de context van Configuration Manager. Gebruik bijvoorbeeld Active Directory Certificate Services en groeps beleid om een webserver certificaat te verlenen. Zie [PKI-certificaat vereisten](../../../plan-design/network/pki-certificate-requirements.md) en [Implementeer het webserver certificaat voor site systemen die IIS uitvoeren](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)voor meer informatie.

Wanneer u de site optie gebruikt om door **Configuration Manager gegenereerde certificaten voor HTTP-site systemen te gebruiken**, kan het beheer punt http zijn. Zie [Enhanced http](../../../plan-design/hierarchy/enhanced-http.md)(Engelstalig) voor meer informatie.

> [!Tip]  
> Als u geen gebruik maakt van verbeterde HTTP en uw omgeving meerdere beheer punten heeft, hoeft u deze niet in HTTPS in te scha kelen voor CMG. Configureer de CMG-beheer punten alleen als **Internet**. Uw on-premises clients proberen deze niet te gebruiken.<!-- SCCMDocs#1676 -->

### <a name="enhanced-http-certificate-for-management-points"></a>Verbeterd HTTP-certificaat voor beheer punten

Wanneer u Enhanced HTTP inschakelt, genereert de site server een zelfondertekend certificaat met de naam **SMS-functie SSL-certificaat**, dat is uitgegeven door het hoofd certificaat voor SMS-verzen ding. Het beheer punt voegt dit certificaat toe aan de IIS-standaard website gebonden aan poort 443.

### <a name="management-point-client-connection-mode-summary"></a>Samen vatting van client verbindings modus Beheer punt

Deze tabellen beschrijven of het beheer punt HTTP of HTTPS vereist, afhankelijk van het type client en de versie van de site.

#### <a name="for-internet-based-clients-communicating-with-the-cloud-management-gateway"></a>Voor clients op Internet die communiceren met de Cloud beheer gateway

Configureer een on-premises beheer punt om verbindingen van de CMG met de volgende client verbindings modus toe te staan:

| Type client   | Beheerpunt |
|------------------|------------------|
| Werkgroep        | E-HTTP-<sup>[Opmerking 1](#bkmk_note1)</sup>, https |
| AD-domein toegevoegd | E-HTTP-<sup>[Opmerking 1](#bkmk_note1)</sup>, https |
| Toegevoegd aan Azure AD  | E-HTTP, HTTPS |
| Hybride join    | E-HTTP, HTTPS |

<a name="bkmk_note1"></a>

> [!Note]  
> **Opmerking 1**: voor deze configuratie moet de client een [certificaat voor client verificatie](#bkmk_clientauth)hebben en worden alleen apparaat gerichte scenario's ondersteund.  

#### <a name="for-on-premises-clients-communicating-with-the-on-premises-management-point"></a>Voor on-premises clients die communiceren met het on-premises beheer punt

Configureer een on-premises beheer punt met de volgende client verbindings modus:

| Type client   | Beheerpunt |
|------------------|------------------|
| Werkgroep        | HTTP, HTTPS |
| AD-domein toegevoegd | HTTP, HTTPS |
| Toegevoegd aan Azure AD  | HTTPS       |
| Hybride join    | HTTP, HTTPS |

> [!NOTE]  
> Clients die lid zijn van een AD-domein ondersteunen zowel apparaat-als gebruikers gerichte scenario's die communiceren met een HTTP-of HTTPS-beheer punt.  
>
> Clients die lid zijn van Azure AD en Hybrid joins kunnen communiceren via HTTP voor apparaat gerichte scenario's, maar moeten E-HTTP of HTTPS hebben om gebruikers gerichte scenario's mogelijk te maken. Anders gedragen ze hetzelfde als werkgroepcomputers.  

#### <a name="legend-of-terms"></a>Legenda van voor waarden

- *Werk groep*: het apparaat is niet gekoppeld aan een domein of Azure AD, maar heeft een [certificaat voor client verificatie](#bkmk_clientauth).
- *AD-domein*: u voegt het apparaat toe aan een on-premises Active Directory domein.
- *Azure AD*: ook wel lid van een Cloud domein genoemd, voegt u het apparaat toe aan een Azure Active Directory-Tenant. Zie apparaten die zijn [toegevoegd aan Azure AD](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join)voor meer informatie.
- *Hybride lid*: u voegt het apparaat toe aan uw on-premises Active Directory en registreert het met uw Azure Active Directory. Zie voor meer informatie [Hybrid Azure AD joined devices](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join-hybrid)(Engelstalig).
- *Http*: voor de eigenschappen van het beheer punt stelt u de client verbindingen in op **http**.
- *Https*: voor de eigenschappen van het beheer punt stelt u de client verbindingen in op **https**.
- *E-http*: op het tabblad site-eigenschappen, **client computer communicatie** , stelt u de site systeem instellingen in op **https of http**en schakelt u de optie voor het **gebruik van door Configuration Manager gegenereerde certificaten voor http-site systemen**in. U configureert het beheer punt voor HTTP, het HTTP-beheer punt is gereed voor HTTP-en HTTPS-communicatie (scenario's voor token verificatie).

    > [!Note]
    > Vanaf versie 1906 wordt dit tabblad **communicatie beveiliging**genoemd.<!-- SCCMDocs#1645 -->

## <a name="azure-management-certificate"></a><a name="bkmk_azuremgmt"></a>Azure-beheer certificaat

*Dit certificaat is vereist voor klassieke service-implementaties. Het is niet vereist voor de implementatie van Azure Resource Manager.*

> [!Important]  
> Vanaf versie 1810 worden de klassieke service-implementaties in azure afgeschaft in Configuration Manager. Begin met het gebruik van Azure Resource Manager-implementaties voor de Cloud beheer gateway. Zie [plan for CMG](plan-cloud-management-gateway.md#azure-resource-manager)voor meer informatie.
>
> Vanaf Configuration Manager versie 1902 is Azure Resource Manager het enige implementatie mechanisme voor nieuwe exemplaren van de Cloud beheer gateway. Dit certificaat is niet vereist in Configuration Manager versie 1902 of hoger.<!-- 3605704 -->

U geeft dit certificaat op in de Azure Portal en wanneer u de CMG maakt in de Configuration Manager-console.

Als u de CMG in azure wilt maken, moet het Configuration Manager service-verbindings punt eerst worden geverifieerd bij uw Azure-abonnement. Wanneer u een klassieke service-implementatie gebruikt, wordt het Azure-beheer certificaat voor deze verificatie gebruikt. Een Azure-beheerder uploadt dit certificaat naar uw abonnement. Wanneer u de CMG in de Configuration Manager-console maakt, moet u dit certificaat opgeven.

Raadpleeg de volgende artikelen in de Azure-documentatie voor meer informatie en instructies voor het uploaden van een beheer certificaat:

- [Cloud Services en beheer certificaten](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)  

- [Een Azure Service Management-certificaat uploaden](https://docs.microsoft.com/azure/azure-api-management-certs)  

> [!IMPORTANT]
> Zorg ervoor dat u de abonnements-ID kopieert die is gekoppeld aan het beheer certificaat. U gebruikt deze voor het maken van de CMG in de Configuration Manager-console.

## <a name="next-steps"></a>Volgende stappen

- [Een cloudbeheergateway instellen](setup-cloud-management-gateway.md)  

- [Veelgestelde vragen over de Cloud beheer gateway](cloud-management-gateway-faq.md)  

- [Beveiliging en privacy voor cloudbeheergateway](security-and-privacy-for-cloud-management-gateway.md)  
