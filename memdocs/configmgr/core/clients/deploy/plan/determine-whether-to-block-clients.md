---
title: Clients blok keren
titleSuffix: Configuration Manager
description: Blok keer client toegang voor systeem beveiliging met behulp van Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 54ef5fbb-521d-4ca5-a1c5-61e6f538d71e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01fd7944d8a6ab726712f6ebeb4cb5374896072
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713238"
---
# <a name="determine-whether-to-block-clients-in-configuration-manager"></a>Bepalen of clients moeten worden geblokkeerd in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Als een client computer of client mobiel apparaat niet meer wordt vertrouwd, kunt u de client blok keren in de System Center 2012 Configuration Manager-console. Geblokkeerde clients worden geweigerd door de Configuration Manager-infra structuur zodat ze niet kunnen communiceren met site systemen om beleid te downloaden, inventaris gegevens te uploaden of status berichten te verzenden.  

 U moet een client blokkeren en zijn blokkering opheffen van zijn toegewezen site, liever dan van een secundaire site of een centrale beheersite.  

> [!IMPORTANT]  
>  Hoewel blok keren in Configuration Manager kan helpen de Configuration Manager-site te beveiligen, moet u niet vertrouwen op deze functie om de site te beveiligen tegen niet-vertrouwde computers of mobiele apparaten als u clients toestaat te communiceren met site systemen door gebruik te maken van HTTP, omdat een geblokkeerde client de site opnieuw zou kunnen samen voegen met een nieuw zelfondertekend certificaat en hardware-ID. Gebruik daarentegen de blokkeringsfunctie om verloren of verdachte opstartmedia te blokkeren die u gebruikt om besturingssystemen te implementeren en wanneer sitesystemen HTTPS-clientverbindingen aanvaarden.  

 Clients die toegang hebben tot de site door gebruik te maken van het ISV Proxy-certificaat kunnen niet geblokkeerd worden. Voor meer informatie over het ISV-proxy certificaat raadpleegt u de Configuration Manager Software Development Kit (SDK).  

 Indien uw sitesystemen HTTPS-clientverbindingen aanvaarden en uw openbare-sleutelinfrastructuur (PKI) een certificaatintrekkingslijst (CRL) ondersteunt, beschouw dan altijd certificaatintrekking als uw eerstelijnsverdediging tegen eventueel verdachte certificaten. Het blok keren van clients in Configuration Manager biedt een tweede verdedigings linie om uw hiërarchie te beschermen.  

##  <a name="considerations-for-blocking-clients"></a><a name="BKMK_Block_vs_CRL"></a> Overwegingen voor het blokkeren van clients  

-   Deze optie is beschikbaar voor HTTP- en HTTPS-clientverbindingen, maar biedt beperkte beveiliging als clients verbinding maken met sitesystemen met HTTP.  

-   Configuration Manager gebruikers met beheerders rechten hebben de bevoegdheid om een client te blok keren en de actie wordt uitgevoerd in de Configuration Manager-console.  

-   Client communicatie wordt alleen geweigerd vanuit de Configuration Manager hiërarchie.  

    > [!NOTE]  
    >  Dezelfde client zou kunnen registreren met een andere Configuration Manager-hiërarchie.  

-   De client wordt onmiddellijk geblokkeerd voor de Configuration Manager-site.  

-   Helpt sitesystemen te beschermen tegen eventueel verdachte computers en mobiele apparaten.  

## <a name="considerations-for-using-certificate-revocation"></a>Overwegingen voor het intrekken van certificaten  

-   De optie is beschikbaar voor HTTPS-verbindingen van Windows-clients als de openbare-sleutelinfrastructuur een certificaatintrekkingslijst (CRL) ondersteunt.  

     Mac-clients voeren altijd een CRL-controle uit en deze functionaliteit kan niet worden uitgeschakeld.  

     Hoewel clients van het mobiele apparaat geen gebruikmaken van certificaat intrekkings lijsten om de certificaten voor site systemen te controleren, kunnen hun certificaten worden ingetrokken en gecontroleerd door Configuration Manager.  

-   Beheerders van open bare-sleutel infrastructuur hebben de bevoegdheid om een certificaat in te trekken en de actie wordt uitgevoerd buiten de Configuration Manager-console.  

-   Clientcommunicatie kan geweigerd worden van elke computer of elk mobiel apparaat dat dit clientcertificaat vereist.  

-   Er is waarschijnlijk een vertraging tussen een certificaat intrekken en sitesystemen die de gewijzigde certificaatintrekkingslijst (CRL) downloaden.  

-   Voor vele PKI-implementaties kan deze vertraging een dag of meer bedragen. In Active Directory Certificate Services bijvoorbeeld is de standaard termijnafloop één week voor een volledige CRM en één dag voor een delta-CRL.  

-   Helpt sitesystemen en clients te beschermen tegen eventueel verdachte computers en mobiele apparaten.  

    > [!NOTE]  
    >  U kunt sitesystemen die IIS uitvoeren verder beschermen tegen onbekende clients door een certificaatvertrouwenslijst (CTL) te configureren in IIS.  
