---
title: Ondersteuning voor Active Directory-domeinen
titleSuffix: Configuration Manager
description: Meer informatie over de vereisten voor een Configuration Manager site systeem in een Active Directory domein.
ms.date: 10/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ab317597633eb432c73d2999590c1859124ddcfd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709612"
---
# <a name="support-for-active-directory-domains-in-configuration-manager"></a>Ondersteuning voor Active Directory domeinen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Alle Configuration Manager-site systemen moeten lid zijn van een ondersteund Active Directory domein. Configuration Manager-client computers kunnen domein leden of werkgroepleden zijn.  

## <a name="requirements-and-limitations"></a>Vereisten en beperkingen

- Domein lidmaatschap is ook van toepassing op site systemen die client beheer op Internet ondersteunen in een perimeter netwerk. (Deze netwerken worden ook wel een DMZ-, gedemilitariseerde-zone en een gescreend subnet genoemd).  

- Het is niet mogelijk om de volgende configuraties te wijzigen voor een computer die als host fungeert voor een site systeemrol:  

  - Domein lidmaatschap, waaronder als u een site systeem uit het domein verwijdert en vervolgens weer lid wordt van hetzelfde domein.

  - Domeinnaam  

  - Computernaam  

  Voordat u deze wijzigingen aanbrengt, moet u de site systeemrol verwijderen. Als u deze wijzigingen wilt aanbrengen in een site server, moet u eerst de site verwijderen. U kunt ook overwegen om een [site server in de passieve modus](../../servers/deploy/configure/site-server-high-availability.md) te maken om deze wijziging op een site server te beheren.

- Configuration Manager ondersteunt het functionaliteits niveau van het domein en forest van Windows Server 2008 R2 of hoger.<!-- SCCMDocs#1853 -->

## <a name="disjoint-namespace"></a><a name="bkmk_Disjoint"></a> Niet-aaneengesloten naamruimte

U kunt Configuration Manager-site systemen en-clients installeren in een domein met een niet- *aaneengesloten naam ruimte*.  

In een niet-aaneengesloten naam ruimte komt het achtervoegsel van de primaire DNS van een computer niet overeen met de Active Directory DNS-domein naam van die computer. Een ander niet-aaneengesloten naam ruimte scenario treedt op als de NetBIOS-domein naam van een domein controller niet overeenkomt met de Active Directory DNS-domein naam.  

### <a name="disjoint-scenarios"></a>Niet-aaneengesloten scenario's

In de volgende secties worden de ondersteunde scenario's voor een niet-aaneengesloten naam ruimte beschreven.  

#### <a name="scenario-1"></a>Scenario 1

Het achtervoegsel van de primaire DNS van de domeincontroller verschilt van de DNS-naam van het Active Directory-domein. Computers die lid van het domein zijn, kunnen ontkoppeld of niet-ontkoppeld zijn.

De domeincontroller is in dit scenario ontkoppeld. Computers die lid zijn van het domein, zoals site servers en computers, kunnen een achtervoegsel voor de primaire DNS hebben die overeenkomt met:

- Het achtervoegsel van de primaire DNS van de domein controller
- De DNS-domein naam van Active Directory

#### <a name="scenario-2"></a>Scenario 2

Een lidcomputers in een Active Directory domein is niet-aaneengesloten, zelfs als de domein controller niet ontkoppeld is.

In dit scenario verschilt het achtervoegsel van de primaire DNS van een site systeem van de Active Directory DNS-domein naam. Het achtervoegsel van de primaire DNS van de domein controller is hetzelfde als de Active Directory DNS-domein naam. Lidcomputers die Configuration Manager-clients zijn, kunnen een primair DNS-achtervoegsel hebben dat overeenkomt met:

- Het achtervoegsel van de primaire DNS van de niet-aaneengesloten site systeem server
- De DNS-domein naam van Active Directory

### <a name="configure-disjoint-namespace"></a>Niet-aaneengesloten naam ruimte configureren

Als u een computer toegang wilt geven tot domein controllers die niet zijn verbonden, wijzigt u het kenmerk **msDS-AllowedDNSSuffixes** Active Directory in de object container Domain. Voeg beide DNS-achtervoegsels toe aan het kenmerk.  

Om ervoor te zorgen dat de *Zoek lijst voor DNS-achtervoegsels* alle DNS-naam ruimten in de organisatie bevat, configureert u de zoek lijst voor elke computer in het niet-aaneengesloten domein. Neem de volgende achtervoegsels op in de lijst met naam ruimten:

- Het achtervoegsel van de primaire DNS van de domein controller
- De DNS-domein naam
- Eventuele aanvullende naam ruimten voor andere servers waarmee Configuration Manager mogelijk communiceert

U kunt groeps beleid gebruiken voor het configureren van de zoek lijst voor **achtervoegsels voor Domain Name System (DNS)** .  

> [!IMPORTANT]  
> Wanneer u verwijst naar een computer in Configuration Manager, voert u de computer in met behulp van het achtervoegsel van de primaire DNS. Dit achtervoegsel moet overeenkomen met de Fully Qualified Domain Name die is geregistreerd als het kenmerk **dnsHostName** in het domein Active Directory en de service principal name die aan het systeem is gekoppeld.  

## <a name="single-label-domains"></a><a name="bkmk_SLD"></a> Domeinen met een enkelvoudig label

Configuration Manager ondersteunt site systemen en clients in een domein met één label wanneer aan de volgende criteria wordt voldaan:  

- Configureer het domein met één label in Active Directory Domain Services met een niet-aaneengesloten DNS-naam ruimte met een geldig domein op het hoogste niveau.  

  **Bijvoorbeeld:** het domein met het enkelvoudige label Contoso is geconfigureerd met een niet-aaneengesloten naamruimte in het DNS contoso.com. Wanneer u het DNS-achtervoegsel in Configuration Manager opgeeft voor een computer in het contoso-domein, geeft u ' Contoso.com ' en niet ' Contoso ' op.  

- De DCOM-verbindingen (Distributed Component Object Model) tussen site servers in de systeem context moeten worden geslaagd met behulp van Kerberos-verificatie.  
