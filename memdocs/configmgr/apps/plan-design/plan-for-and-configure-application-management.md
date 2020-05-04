---
title: Toepassings beheer plannen
titleSuffix: Configuration Manager
description: Implementeer en configureer de vereiste afhankelijkheden voor het implementeren van toepassingen in Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 03fda62774b930a1cc3603415f3b872050b9cb71
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709941"
---
# <a name="plan-for-and-configure-application-management-in-configuration-manager"></a>Toepassings beheer plannen en configureren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik de informatie in dit artikel om u te helpen bij het implementeren van de vereiste afhankelijkheden voor het implementeren van toepassingen in Configuration Manager.  



## <a name="dependencies-external-to-configuration-manager"></a>Afhankelijkheden extern aan Configuration Manager  


### <a name="internet-information-services-iis"></a>Internet Information Services (IIS)

IIS is vereist op de servers waarop de volgende site systeem rollen worden uitgevoerd:

- Beheerpunt  
- Distributiepunt  

Zie voor meer informatie [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Vereisten voor sites en sitesystemen).  

> [!Note]  
> De Application Catalog vereist ook IIS. De Silverlight-gebruikers ervaring wordt echter niet ondersteund op de huidige branch-versie 1806. Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  
>
> Raadpleeg voor meer informatie de volgende artikelen:
>
> - [Software Center configureren](plan-for-software-center.md#bkmk_userex)
> - [Verwijderde en afgeschafte functies](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  


### <a name="certificates-on-code-signed-applications-for-mobile-devices"></a>Certificaten voor toepassingen die zijn ondertekend met een code voor mobiele apparaten

Wanneer u toepassingen codeert om ze te implementeren op mobiele apparaten, moet u geen certificaat gebruiken dat is gegenereerd met een sjabloon van versie 3 (**Windows Server 2008, Enter prise Edition**). Met deze certificaat sjabloon wordt een certificaat gemaakt dat niet compatibel is met Configuration Manager toepassingen voor mobiele apparaten.

Als u Active Directory Certificate Services gebruikt om toepassingen voor mobiele apparaten te ondertekenen, moet u geen certificaat sjabloon van versie 3 gebruiken.


### <a name="audit-sign-in-events-for-user-device-affinity"></a>Aanmeldings gebeurtenissen voor gebruikers affiniteit met apparaat controleren  

Als u automatisch affiniteiten tussen gebruikers en apparaten wilt maken, configureert u clients om aanmeldings gebeurtenissen te controleren.

Om de automatische gebruikers affiniteit van apparaten te bepalen, leest de Configuration Manager-client aanmeldings gebeurtenissen van het type **geslaagd** vanuit het Windows-beveiligings logboek. Schakel deze gebeurtenissen in met de volgende twee controle beleidsregels:

- **Aanmeldingsgebeurtenissen voor accounts controleren**
- **Aanmeldingsgebeurtenissen controleren**

Als u automatisch relaties tussen gebruikers en apparaten wilt maken, moet u ervoor zorgen dat deze twee instellingen zijn ingeschakeld op clientcomputers. U kunt het Windows-groepsbeleid gebruiken om deze instellingen te configureren.

Zie [gebruikers en apparaten koppelen met gebruikers affiniteit met apparaat](../deploy-use/link-users-and-devices-with-user-device-affinity.md)voor meer informatie over de gebruikers affiniteit van apparaten.  



## <a name="configuration-manager-dependencies"></a>Configuration Manager-afhankelijkheden


### <a name="management-point"></a>Beheerpunt

Clients maken contact met een beheer punt om client beleid te downloaden om inhoud te zoeken.

Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers.

In versie 1902 en eerder kunnen clients het beheer punt gebruiken om verbinding te maken met de toepassings catalogus. Als clients geen toegang hebben tot een beheer punt, kunnen ze de toepassings catalogus niet gebruiken.

> [!Note]  
> Met ingang van versie 1806 zijn de functies van de Application Catalog niet langer vereist voor het weer geven van gebruikers beschik bare toepassingen in Software Center. Zie [Software Center configureren](plan-for-software-center.md#bkmk_userex)voor meer informatie.<!--1358309-->  
>
> Vanaf versie 1906 kunt u geen nieuwe functies van de toepassings catalogus installeren. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  
  

### <a name="distribution-point"></a>Distributiepunt

Voordat u toepassingen kunt implementeren op-clients, moet u ten minste één distributie punt in de hiërarchie hebben. Op de siteserver is standaard een siterol van het distributiepunt ingeschakeld tijdens een standaardinstallatie. Het aantal en de locatie van de distributie punten zijn afhankelijk van de specifieke vereisten van uw omgeving.

Zie [inhoud en infra structuur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)voor inhoud beheren voor meer informatie over het installeren van distributie punten en het beheren van inhoud.  


### <a name="reporting-services-point"></a>Reporting Services-punt

Als u de rapporten in Configuration Manager voor toepassings beheer wilt gebruiken, moet u eerst een Reporting Services-punt installeren en configureren.

Zie [Introduction to Reporting](../../core/servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie.  


### <a name="client-settings"></a>Clientinstellingen

Veel client instellingen bepalen hoe de client toepassingen en de gebruikers ervaring op het apparaat installeert. Deze client instellingen omvatten de volgende groepen:

- Computer agent  
- Computer opnieuw opstarten  
- Software Center  
- Software-implementatie  
- Affiniteit van gebruiker en apparaat  

Raadpleeg voor meer informatie de volgende artikelen:

- [Clientinstellingen](../../core/clients/deploy/about-client-settings.md)  
- [Clientinstellingen configureren](../../core/clients/deploy/configure-client-settings.md)  


### <a name="security-permissions-for-application-management"></a>Beveiligingsmachtigingen voor toepassingsbeheer

- De beveiligingsrol **toepassings Auteur** bevat de vereiste machtigingen voor het maken, wijzigen en buiten gebruik stellen van toepassingen.  

- De beveiligingsrol **beheerder toepassingsimplementaties** omvat de vereiste machtigingen voor het implementeren van toepassingen.  

- De beveiligingsrol **toepassings beheerder** heeft alle machtigingen van zowel de auteur van de **toepassing** als de beveiligings rollen van de **beheerder toepassingsimplementaties** .  

Zie [op rollen gebaseerd beheer configureren](../../core/servers/deploy/configure/configure-role-based-administration.md)voor meer informatie.  


### <a name="app-v-46-sp1-or-later-client-to-run-virtual-applications"></a>App-V 4.6 SP1-client of hoger om virtuele toepassingen uit te voeren

Als u virtuele toepassingen in Configuration Manager wilt maken, installeert u app-V 4,6 SP1 of hoger op apparaten.

Voordat u virtuele toepassingen implementeert, moet u ook de app-V-client bijwerken met de hotfix die wordt beschreven in het [Microsoft ondersteuning-artikel 2645225](https://support.microsoft.com/help/2645225).  


### <a name="application-catalog"></a>Toepassings catalogus

> [!Important]  
> Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.. Zie [de Application Catalog verwijderen](#bkmk_remove-appcat)voor meer informatie.  

#### <a name="application-catalog-web-service-point"></a>Application Catalog-webservicepunt

Het Application Catalog-webservicepunt is een site systeemrol die informatie biedt over de beschik bare software van uw software bibliotheek naar de Application catalog-website die gebruikers openen.

Zie [de Toepassingscatalogus installeren en configureren](#bkmk_appcat)voor meer informatie over het configureren van deze site systeemrol.  

#### <a name="application-catalog-website-point"></a>Application catalog-website punt

Het Application catalog-website punt is een site systeemrol die gebruikers een lijst met beschik bare software verschaft.

Zie [de Toepassingscatalogus installeren en configureren](#bkmk_appcat)voor meer informatie over het configureren van deze site systeemrol.

#### <a name="discovered-user-accounts-for-application-catalog"></a>Gedetecteerde gebruikers accounts voor de toepassings catalogus

Configuration Manager moet eerst gebruikers accounts detecteren voordat gebruikers toepassingen uit de toepassings catalogus kunnen weer geven en aanvragen. Zie [detectie uitvoeren](../../core/servers/deploy/configure/run-discovery.md)voor meer informatie.  



## <a name="configure-software-center"></a><a name="bkmk_userex"></a>Software Center configureren  

Zie voor meer informatie over het configureren en merken van software Center [plannen voor Software Center](plan-for-software-center.md).


## <a name="remove-the-application-catalog"></a><a name="bkmk_remove-appcat"></a>De toepassings catalogus verwijderen

<!-- SCCMDocs-pr issue 3051 -->

Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910. Zie [verwijderde en afgeschafte functies](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)voor meer informatie. De volgende lijst bevat een overzicht van de wijzigingen:

- Vanaf versie 1806 wordt de **Silverlight-gebruikers ervaring** voor het Application catalog-website punt niet meer ondersteund.<!--1358309--> De rol Application Catalog-webservicepunt is niet langer *vereist*, maar wordt wel *ondersteund*.

- Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren.

- Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  

Deze herhaalde verbeteringen voor Software Center en het beheer punt zijn het vereenvoudigen van uw infra structuur en de nood zaak van de toepassings catalogus voor door gebruikers beschik bare implementaties te verwijderen. Software Center kan alle app-implementaties leveren zonder de Application Catalog. Als u TLS 1,2 inschakelt en HTTP met de toepassings catalogus gebruikt, kunnen gebruikers ook geen gebruikers gerichte, beschik bare implementaties zien. Werk Configuration Manager naar versie 1906 of hoger om deze verbeteringen te voor komen.

1. Alle clients bijwerken naar versie 1806 of hoger. Versie 1906 wordt aanbevolen.  

1. Stel huisstijl voor Software Center in, in plaats van in de eigenschappen van de Application catalog-website functie. Zie [client instellingen voor Software Center](../../core/clients/deploy/about-client-settings.md#software-center)voor meer informatie.  

1. Controleer de standaard-en aangepaste client instellingen. Controleer in de groep **computer agent** of het **standaard toepassingscatalogus website punt** is `(none)`.  

    In versie 1902 en eerder wordt de client alleen overgeschakeld naar het gebruik van het beheer punt als er geen Application Catalog-rollen in de hiërarchie zijn. Anders blijven clients een van de exemplaren van de catalogus met toepassingen in de hiërarchie gebruiken. Dit gedrag is van toepassing op afzonderlijke primaire sites.  

1. De **Application Catalog** -website en **Application Catalog** -site systeem rollen verwijderen van alle primaire sites.

Nadat u de functies van de toepassings catalogus hebt verwijderd, wordt software Center gestart met behulp van het beheer punt voor door de gebruiker beschik bare implementaties. In versie 1902 en eerder kan het tot 65 minuten duren voordat deze wijziging is doorgevoerd. Als u dit gedrag op een specifieke client wilt controleren, `SCClient_<username>.log`bekijkt u de en zoekt u naar een vermelding die lijkt op de volgende regel:

`Using endpoint Url: https://mp.contoso.com/CMUserService_WindowsAuth, Windows authentication`


## <a name="install-and-configure-the-application-catalog"></a><a name="bkmk_appcat"></a>De toepassings catalogus installeren en configureren  

> [!Important]  
> Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910. Zie [de Application Catalog verwijderen](#bkmk_remove-appcat)voor meer informatie.  

### <a name="step-1-web-server-certificate-for-https"></a>Stap 1: webserver certificaat voor HTTPS

Als u HTTPS-verbindingen gebruikt, implementeert u een webserver certificaat op de site systeem servers voor het Application catalog-website punt en het Application Catalog-webservicepunt.

Als u wilt dat clients de Application Catalog vanaf internet gebruiken, implementeert u een webserver certificaat op ten minste één beheer punt. Configureer deze voor client verbindingen van het internet.

Zie [PKI-certificaat vereisten](../../core/plan-design/network/pki-certificate-requirements.md)voor meer informatie over certificaat vereisten.  


### <a name="step-2-client-authentication-certificate-for-https"></a>Stap 2: certificaat voor client verificatie voor HTTPS

Als u een PKI-client certificaat gebruikt voor verbindingen met beheer punten, implementeert u een certificaat voor client verificatie op client computers. Hoewel clients geen PKI-client certificaat gebruiken om verbinding te maken met de toepassings catalogus, moeten ze verbinding maken met een beheer punt voordat ze de toepassings catalogus kunnen gebruiken.

Implementeer een certificaat voor client verificatie op client computers in de volgende scenario's:

- Alle beheer punten op het intranet accepteren alleen HTTPS-client verbindingen.
- Clients maken verbinding met de toepassings catalogus via internet.

Zie [PKI-certificaat vereisten](../../core/plan-design/network/pki-certificate-requirements.md)voor meer informatie over certificaat vereisten.  


### <a name="step-3-install-and-configure-the-application-catalog-roles"></a>Stap 3: de functies van de toepassings catalogus installeren en configureren

Installeer zowel het Application Catalog-webservicepunt als de Application catalog-website rollen in dezelfde site. U hoeft ze niet op dezelfde server of in hetzelfde Active Directory forest te installeren. Het Application Catalog-webservicepunt moet zich echter in hetzelfde forest bevinden als de site database.

Zie voor meer informatie over server plaatsing [plannen voor site systeem servers en site systeem rollen](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

> [!NOTE]  
> Installeer de Application Catalog op een primaire site. U kunt deze niet installeren op een secundaire site of de centrale beheer site.  

Installeer de Application Catalog op een nieuwe site systeem server of op een bestaande server in de site. Zie [site systeem rollen installeren](../../core/servers/deploy/configure/install-site-system-roles.md)voor meer informatie over de algemene procedure. Selecteer in de wizard om een site systeemrol toe te voegen of een site systeem server te maken de volgende rollen in de lijst:  

- **Application Catalog-webservicepunt**  
- **Application catalog-website punt**  

> [!TIP]  
> Als u wilt dat client computers de Application Catalog via internet gebruiken, geeft u de Internet Fully Qualified Domain Name (FQDN) op.  

#### <a name="verify-the-installation-of-these-site-system-roles"></a>De installatie van deze site systeem rollen controleren  

- Statusberichten: gebruik de onderdelen **SMS_PORTALWEB_CONTROL_MANAGER** en **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Bijvoorbeeld, status-ID **1015** voor **SMS_PORTALWEB_CONTROL_MANAGER** bevestigt site Component Manager dat het Application catalog-website punt is geïnstalleerd.  

- Logboekbestanden: zoek naar **SMSAWEBSVCSetup.log** en **SMSPORTALWEBSetup.log**.  

    Zoek naar de logboek bestanden **awebsvcMSI. log** en **portlwebMSI. log** voor meer informatie.  


### <a name="step-4-configure-client-settings"></a>Stap 4: client instellingen configureren

Als u wilt dat alle gebruikers dezelfde instellingen hebben, configureert u de standaard client instellingen. Configureer anders aangepaste clientinstellingen voor specifieke verzamelingen.

Raadpleeg voor meer informatie de volgende artikelen:

- [Clientinstellingen](../../core/clients/deploy/about-client-settings.md)  
    - Computer agent  
    - Computer opnieuw opstarten  
    - Software Center  
    - Software-implementatie  
    - Affiniteit van gebruiker en apparaat  
- [Clientinstellingen configureren](../../core/clients/deploy/configure-client-settings.md)  

De Configuration Manager-client configureert apparaten met deze instellingen wanneer de volgende keer het client beleid wordt gedownload. Zie [clients beheren](../../core/clients/manage/manage-clients.md)om het ophalen van beleid voor één client te activeren.


### <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Stap 5: controleren of de toepassings catalogus operationeel is

Gebruik de volgende procedures om te controleren of de toepassings catalogus operationeel is.

> [!NOTE]  
> De gebruikers ervaring van de toepassings catalogus vereist micro soft Silverlight. Als u de Application Catalog rechtstreeks vanuit een browser gebruikt, controleert u eerst of micro soft Silverlight op de computer is geïnstalleerd.  

> [!TIP]  
> Ontbrekende vereisten zijn een van de meest voorkomende redenen waarom de toepassings catalogus onjuist werkt na de installatie. Bevestig de vereisten voor de rol voor de Application Catalog-site systeem rollen. Zie voor meer informatie [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Vereisten voor sites en sitesystemen).  

Voer in een browser het adres van de Application catalog-website in. Controleer of op de webpagina de drie tabbladen worden weer gegeven: **toepassingscatalogus**, **mijn toepassings aanvragen**en **mijn apparaten**.  

Gebruik het juiste adres voor de toepassings catalogus in de volgende lijst, waarbij `<server>` de computer naam, intranet-FQDN of Internet-FQDN:  

- HTTPS-client verbindingen en standaard instellingen van de site systeemrol:`https://<server>/CMApplicationCatalog`  

- HTTP-client verbindingen en standaard instellingen voor de site systeemrol:`http://<server>/CMApplicationCatalog`  

- HTTPS-client verbindingen en aangepaste instellingen voor de site systeemrol:`https://<server>:<port>/<web application name>`  

- HTTP-client verbindingen en aangepaste instellingen voor de site systeemrol:`http://<server>:<port>/<web application name>`  

> [!NOTE]  
> Als u bent aangemeld bij het apparaat met een domein beheerders account, worden in de Configuration Manager-client geen meldings berichten weer gegeven. Bijvoorbeeld berichten die aangeven dat er nieuwe software beschikbaar is.  
