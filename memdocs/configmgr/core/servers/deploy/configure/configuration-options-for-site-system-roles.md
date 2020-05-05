---
title: Opties voor de site systeemrol
titleSuffix: Configuration Manager
description: Raadpleeg dit artikel voor meer informatie over Configuration Manager-site systeem rollen die niet noodzakelijkerwijs zelf verklaren.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9dfe9e0cb2ecefc636c67cf127e596fd1ad2bfa4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721085"
---
# <a name="configuration-options-for-site-system-roles-in-configuration-manager"></a>Configuratie opties voor site systeem rollen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

De meeste configuratie opties voor Configuration Manager site systeem rollen zijn zelf uitleg of worden in de wizard of dialoog vensters uitgelegd wanneer u ze configureert. In de volgende secties worden site systeem rollen uitgelegd waarvan de instellingen mogelijk aanvullende informatie nodig hebben.  


## <a name="application-catalog-website-point"></a><a name="BKMK_ApplicationCatalog_Website"></a>Application catalog-website punt  

> [!Important]
> De Silverlight-gebruikers ervaring van de toepassings catalogus wordt niet ondersteund vanaf de huidige branch-versie 1806. Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  
>
> Raadpleeg voor meer informatie de volgende artikelen:
>
> - [Software Center configureren](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Verwijderde en afgeschafte functies](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Zie [toepassings beheer plannen en configureren](../../../../apps/plan-design/plan-for-and-configure-application-management.md)voor meer informatie over het instellen van het Application catalog-website punt.  


## <a name="application-catalog-web-service-point"></a><a name="BKMK_ApplicationCatalog_WebService"></a>Application Catalog-webservicepunt  

> [!Important]
> De Silverlight-gebruikers ervaring van de toepassings catalogus wordt niet ondersteund vanaf de huidige branch-versie 1806. Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  
>
> Raadpleeg voor meer informatie de volgende artikelen:
>
> - [Software Center configureren](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Verwijderde en afgeschafte functies](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Zie [toepassings beheer plannen en configureren](../../../../apps/plan-design/plan-for-and-configure-application-management.md)voor meer informatie over het instellen van het toepassingscatalogus-webservicepunt.  


## <a name="certificate-registration-point"></a><a name="BKMK_CertificateRegistrationPoint"></a>Certificaat registratiepunt  

Zie [Inleiding tot certificaat profielen](../../../../protect/deploy-use/introduction-to-certificate-profiles.md)voor meer informatie over het instellen van het certificaat registratiepunt.  


## <a name="distribution-point"></a><a name="BKMK_Distribution_Point"></a> Distributiepunt  

Zie [inhoud en infra structuur](manage-content-and-content-infrastructure.md)voor inhoud beheren voor meer informatie over het instellen van het distributie punt voor inhouds implementatie.  

Zie [PXE gebruiken om Windows via het netwerk te implementeren](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md)voor meer informatie over het instellen van het distributie punt voor PXE-implementaties.  

Zie [multi cast gebruiken om Windows via het netwerk te implementeren](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md)voor meer informatie over het instellen van het distributie punt voor multi cast-implementaties.  

### <a name="install-and-configure-iis-if-required-by-configuration-manager"></a>Installeer en Configureer IIS indien vereist door Configuration Manager

Selecteer deze optie als Configuration Manager u IIS op het site systeem wilt installeren en instellen als dat nog niet is gebeurd. IIS moet op alle distributie punten zijn geïnstalleerd en u moet deze instelling selecteren om door te gaan in de wizard.  

### <a name="site-system-installation-account"></a>Installatie account site systeem

Voor distributie punten die op een site server zijn geïnstalleerd, wordt alleen het computer account van de site server ondersteund voor gebruik als het installatie account van het site systeem. Zie [accounts](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)voor meer informatie.  


## <a name="enrollment-point"></a><a name="BKMK_Enrollment_Point"></a> Inschrijvingspunt  

Inschrijvings punten worden gebruikt om macOS-computers te installeren en apparaten te registreren die u beheert met on-premises Mobile Device Management. Raadpleeg voor meer informatie de volgende artikelen:  

- [Clients op Macs implementeren](../../../clients/deploy/deploy-clients-to-macs.md)  

- [Hoe gebruikers apparaten inschrijven met on-premises MDM](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

### <a name="allowed-connections"></a>Toegestane verbindingen

De HTTPS-instelling wordt automatisch geselecteerd en vereist een PKI-certificaat op de server voor Server verificatie voor het inschrijvings proxy punt en versleuteling van gegevens via SSL. Zie [PKI-certificaat vereisten](../../../plan-design/network/pki-certificate-requirements.md)voor meer informatie.  

Zie [het webserver certificaat implementeren voor site systemen waarop IIS wordt uitgevoerd](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)voor een voor beeld van de implementatie van het server certificaat en informatie over het configureren van deze service in IIS.  


## <a name="enrollment-proxy-point"></a><a name="BKMK_Enrollment_Proxy_Point"></a> Proxypunt voor inschrijving  

Zie [hoe gebruikers apparaten inschrijven met on-premises MDM](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)voor meer informatie over het instellen van een inschrijvings proxy punt voor mobiele apparaten.  

### <a name="client-connections"></a>Clientverbindingen

De HTTPS-instelling wordt automatisch geselecteerd. Hiervoor zijn de volgende PKI-certificaten vereist op de server:

- Voor Server verificatie voor mobiele apparaten en Mac-computers die u registreert met Configuration Manager
- Voor versleuteling van gegevens over Secure Sockets Layer (SSL)

Zie [PKI-certificaat vereisten](../../../plan-design/network/pki-certificate-requirements.md)voor meer informatie over de certificaat vereisten.  

Zie [het webserver certificaat implementeren voor site systemen waarop IIS wordt uitgevoerd](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)voor een voor beeld van de implementatie van het server certificaat en informatie over het configureren van deze service in IIS.  


## <a name="fallback-status-point"></a><a name="BKMK_Fallback_Status_Point"></a>Terugval status punt  

### <a name="number-of-state-messages-and-throttle-interval-in-seconds"></a>Aantal status berichten en vertragings interval (in seconden)

De standaard instellingen voor deze opties zijn 10.000 status berichten en 3.600 seconden voor het vertragings interval. Hoewel deze instellingen in de meeste gevallen voldoende zijn, moet u deze mogelijk wijzigen wanneer aan de volgende voor waarden wordt voldaan:  

- Het terugval status punt accepteert alleen verbindingen van het intranet.  

- U gebruikt het terugval status punt tijdens een implementatie van de client voor een groot aantal computers.  

In dit scenario kan een doorlopende stroom van status berichten een achterstand veroorzaken van status berichten die het gebruik van hoge processors op de site server gedurende een langere periode veroorzaken. Daarnaast ziet u mogelijk niet de meest recente informatie over de client implementatie in de Configuration Manager-console en in de client implementatie rapporten.  

Deze instellingen voor het terugval status punt zijn ontworpen om te worden ingesteld voor status berichten die tijdens de client implementatie worden gegenereerd. De instellingen zijn niet bedoeld om te worden ingesteld voor problemen met client communicatie, zoals wanneer clients op Internet geen verbinding kunnen maken met het beheer punt op internet. Omdat het terugval status punt deze instellingen niet alleen kan Toep assen op de status berichten die tijdens de client implementatie worden gegenereerd, configureert u deze instellingen niet wanneer het terugval status punt verbindingen van het internet accepteert.  

Elke computer waarop de Configuration Manager-client is geïnstalleerd, verzendt de volgende vier status berichten naar het terugval status punt:  

- Client implementatie is gestart  

- Client implementatie is voltooid  

- Client toewijzing is gestart  

- Client toewijzing is voltooid  

Computers die niet kunnen worden geïnstalleerd of die de Configuration Manager-client toewijzen, verzenden extra status berichten.  

Als u bijvoorbeeld de Configuration Manager client op 20.000 computers implementeert, kan de implementatie 80.000 status berichten naar het terugval status punt verzenden. Omdat de standaard 10.000 configuratie voor het beperken van de status berichten elke 3.600 seconden (1 uur) kan worden verzonden naar het terugval status punt, kunnen status berichten een achterstand voor het terugval status punt worden. Denk ook na over de beschik bare netwerk bandbreedte tussen het terugval status punt en de site server en de verwerkings kracht van de site server om veel status berichten te verwerken.  

Als u deze problemen wilt voor komen, moet u rekening houden met een toename van het aantal status berichten en een afname van het vertragings interval.  

Stel de vertragings waarden voor het terugval status punt opnieuw in als aan een van de volgende voor waarden wordt voldaan:  

- U berekent dat de huidige vertragings waarden hoger zijn dan vereist voor het verwerken van status berichten van het terugval status punt.  

- U ziet dat de huidige beperkings instellingen een hoog processor gebruik maken op de site server.  

Wijzig de instellingen voor de beperkings instellingen voor het terugval status punt niet, tenzij u de gevolgen begrijpt. Wanneer u de beperkings instellingen bijvoorbeeld verhoogt naar hoog, kan het processor gebruik op de site server worden verhoogd tot hoog, waardoor alle site bewerkingen worden vertraagd.  
