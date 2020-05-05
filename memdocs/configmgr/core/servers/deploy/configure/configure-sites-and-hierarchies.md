---
title: Sites en hiërarchieën configureren
titleSuffix: Configuration Manager
description: Raadpleeg deze controle lijst om ervoor te zorgen dat u rekening houdt met de meest voorkomende configuraties die van invloed zijn op zowel sites als hiërarchieën.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e996c31a4f1aaa9224e4c6d1d435f79adf7ac23c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720994"
---
# <a name="configure-sites-and-hierarchies-for-configuration-manager"></a>Sites en hiërarchieën configureren voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Nadat u uw eerste Configuration Manager-site hebt geïnstalleerd of extra sites aan uw hiërarchie hebt toegevoegd, gebruikt u deze controle lijst om ervoor te zorgen dat u rekening houdt met de meest voorkomende configuraties die van invloed zijn op zowel sites als hiërarchieën.  

De volgende configuratie notities zijn van toepassing op de meeste implementaties:  

- Sommige opties zijn gebaseerd op elkaar, zoals Active Directory forest-detectie, grenzen en grens groepen.  

- Verschillende configuraties hebben standaard waarden om te gebruiken zonder configuratie wijzigingen, ten minste aan het begin.  

- Voor andere configuraties, zoals grens groepen en distributiepunten groepen, moet u deze configureren voordat u kunt gebruiken.  

| Bewerking | Details |  
|------------|-------------|  
| Beheer op basis van rollen configureren | Beheer toewijzingen gescheiden om te bepalen welke gebruikers met beheerders rechten verschillende objecten en gegevens in uw Configuration Manager omgeving kunnen weer geven en beheren.<br /><br /> Configuraties voor beheer op basis van rollen worden gedeeld met alle sites in een hiërarchie.   <br/><br/>Zie [op rollen gebaseerd beheer configureren](configure-role-based-administration.md)voor meer informatie. |  
| Site gegevens publiceren naar Active Directory Domain Services | Maak het eenvoudig voor clients om services te vinden en site bronnen efficiënt te gebruiken.<br /><br /> [Breid eerst het Active Directory schema](../../../plan-design/network/extend-the-active-directory-schema.md)uit. Configureer vervolgens elke site afzonderlijk om [site gegevens te publiceren](publish-site-data.md) |  
| Een serviceverbindingspunt configureren | Plan het installeren en configureren van het service verbindings punt op de site op het hoogste niveau van uw hiërarchie. Zie [about the Service Connection Point](about-the-service-connection-point.md)(Engelstalig) voor meer informatie. |  
| Sitesysteemrollen toevoegen | Installeer een of meer extra site systeem rollen voor afzonderlijke sites. Zie [site systeem rollen toevoegen](add-site-system-roles.md)voor meer informatie. |  
| Sitegrenzen en grensgroepen configureren | Geef grenzen op die netwerk locaties op uw intranet definiëren die apparaten kunnen bevatten die u wilt beheren. Configureer vervolgens grens groepen, zodat clients op deze netwerk locaties Configuration Manager-resources kunnen vinden. Zie [site grenzen en grens groepen definiëren](define-site-boundaries-and-boundary-groups.md)voor meer informatie. |  
| Distributiepuntengroepen configureren | Configureer logische groepen van distributie punten om het beheren van implementaties eenvoudiger te maken. Zie [distributiepunt groepen beheren](install-and-configure-distribution-points.md#bkmk_manage)voor meer informatie. |  
| Detectie uitvoeren | Voer de detectie uit om resources in uw netwerk te zoeken, zoals de netwerk infrastructuur, apparaten en gebruikers.<br /><br /> Zie [detectie uitvoeren](run-discovery.md)voor meer informatie. |  
| Redundantie en capaciteit toevoegen voor beheerders | Installeer extra SMS-providers en Configuration Manager-consoles om capaciteit uit te breiden voor beheerders om uw infra structuur te beheren:<br /><br /> **Installeer extra sms-providers** om redundantie te bieden voor console-en API-verbindingen met de site. Zie [Manage the SMS provider](../../manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider)(Engelstalig) voor meer informatie.<br /><br /> **Installeer aanvullende Configuration Manager-consoles** om toegang te bieden tot extra gebruikers met beheerders rechten. Zie [Configuration Manager-consoles installeren](../install/install-consoles.md)voor meer informatie. |  
| Siteonderdelen configureren | Configureer op elke site site onderdelen om het gedrag van site systeem rollen en site status rapportage te wijzigen. Zie [site onderdelen](site-components.md)voor meer informatie. |  
| Aangepaste verzamelingen maken | Het gebruik van informatie die de site detecteert over apparaten en gebruikers, het maken van aangepaste verzamelingen van objecten om toekomstige beheer taken te vereenvoudigen. Zie [verzamelingen maken](../../../clients/manage/collections/create-collections.md)voor meer informatie. |  
| Instellingen configureren voor het beheren van implementaties met een hoog risico | Configureer instellingen op een site om beheerders te waarschuwen wanneer ze een implementatie met een hoog risico maken. Zie [instellingen voor het beheren van implementaties met een hoog risico](../../manage/settings-to-manage-high-risk-deployments.md)voor meer informatie. |  
| Databasereplica's voor beheerpunten configureren | Configureer een database replica om de processor belasting die door beheer punten op de site database server wordt geplaatst, te verminderen als service aanvragen van clients. Zie [database replica's voor beheer punten](database-replicas-for-management-points.md)voor meer informatie. |  
| Een SQL Server AlwaysOn-beschikbaarheids groep configureren | Configureer beschikbaarheids groepen als oplossingen voor hoge Beschik baarheid en herstel na nood gevallen voor het hosten van de site database op primaire sites en de centrale beheer site. Zie [SQL Server AlwaysOn voor een Maxi maal beschik bare site database](sql-server-alwayson-for-a-highly-available-site-database.md)voor meer informatie. |  
| Replicatie tussen sites wijzigen | Zie [gegevens overdracht tussen sites](../../../plan-design/hierarchy/data-transfers-between-sites.md) voor meer informatie over de volgende onderwerpen:<br /><br /> [Replicatie op basis](../../../plan-design/hierarchy/file-based-replication.md) van een bestand tussen secundaire sites configureren<br /><br /> [Database replicatie koppelingen](../../../plan-design/hierarchy/database-replication.md) configureren<br /><br /> [Gedistribueerde weer gaven](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) configureren |  
| Site servers configureren in de passieve modus | Vanaf versie 1806 configureert u een site server in de passieve modus voor elke primaire site en de centrale beheer site. Deze functie biedt een Maxi maal beschik bare site server. Zie [hoge Beschik baarheid van site server](site-server-high-availability.md)voor meer informatie. |  
