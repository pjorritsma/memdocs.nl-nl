---
title: Rapportage plannen
titleSuffix: Configuration Manager
description: Van installatie Details tot beveiliging en netwerk bandbreedte is het belang rijk om te plannen voor rapportage in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ff920c84-d5c8-458c-b67f-bc7219b05690
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2621a6a364734a1146700aa8eef8fded3a6e58ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713679"
---
# <a name="plan-for-reporting-in-configuration-manager"></a>Rapportage plannen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Rapportage in Configuration Manager voorziet in een set hulpprogram ma's en bronnen waarmee u de geavanceerde rapportage mogelijkheden van SQL Server Reporting Services of Power BI Report Server kunt gebruiken. Gebruik de volgende secties om u te helpen bij het plannen van rapportage in Configuration Manager.

## <a name="where-to-install-the-reporting-services-point"></a>Waar het Reporting Services-punt moet worden geïnstalleerd?

Wanneer u Configuration Manager-rapporten uitvoert op een site, hebben de rapporten toegang tot de informatie in de site database waarin deze verbinding maakt. U kunt met behulp van de volgende rubrieken bepalen waar u het Reporting Services-punt wilt installeren en welke gegevensbron u wilt gebruiken.

> [!NOTE]
> Zie [site systeem rollen toevoegen](../deploy/configure/add-site-system-roles.md)voor meer informatie over het plannen van site systemen in Configuration Manager.

### <a name="supported-site-system-servers"></a> Ondersteunde sitesysteemservers

U kunt het Reporting Services-punt op een centrale beheer site (CA'S) en primaire sites installeren. Het werkt op meerdere site systemen op een site en op andere sites in de hiërarchie. Configuration Manager biedt geen ondersteuning voor het Reporting Services-punt op secundaire sites. Het eerste Reporting Services-punt op een site wordt ingesteld als de standaard rapport server. U kunt meer Reporting Services-punten toevoegen aan een site, maar Configuration Manager rapporten actief gebruikmaken van de standaard rapport server op elke site. Installeer het Reporting Services-punt op de site server of een extern site systeem. Gebruik SQL Server Reporting Services op een externe site systeem server voor de beste prestaties.

### <a name="data-replication-considerations"></a> Overwegingen voor gegevensreplicatie

U kunt de volgende factoren overwegen om te kunnen bepalen waar u uw Reporting Services-punten wilt installeren:

- Een Reporting Services-punt met de CAS-Data Base als rapport gegevens bron heeft toegang tot alle globale en site gegevens in de Configuration Manager-hiërarchie. Als u rapporten nodig hebt die site gegevens voor meerdere sites in een hiërarchie bevatten, kunt u overwegen om het Reporting Services-punt op een site systeem op de CAS te installeren. Gebruik vervolgens de bijbehorende data base als rapport gegevens bron.

- Een Reporting Services-punt met een onderliggende primaire site database als rapport gegevens bron heeft alleen toegang tot globale gegevens en site gegevens voor de lokale primaire site en eventuele onderliggende secundaire sites. Site gegevens voor andere primaire sites in de Configuration Manager-hiërarchie worden niet gerepliceerd naar deze primaire site. Reporting Services heeft geen toegang tot site gegevens voor andere primaire sites. Als u rapporten nodig hebt die site gegevens bevatten voor een specifieke primaire site of globale gegevens, en u niet wilt dat de gebruiker toegang heeft tot site gegevens van andere primaire sites, installeert u een Reporting Services-punt op een site systeem op de primaire site. Gebruik vervolgens de data base van de primaire site als rapport gegevens bron.

Zie [typen gegevens](../../plan-design/hierarchy/database-replication.md#types-of-data)voor meer informatie over globale en site gegevens.

### <a name="network-bandwidth-considerations"></a>Overwegingen voor netwerkbandbreedte

Afhankelijk van hoe u de site configureert, communiceren site systemen in dezelfde site met elkaar met behulp van SMB (Server Message Block), HTTP of HTTPS. Configuration Manager beheert deze communicatie niet. Deze kan op elk gewenst moment zonder netwerk bandbreedte regeling worden uitgevoerd. Controleer de beschik bare netwerk bandbreedte voordat u de rol Reporting Services-punt op een site systeem installeert.

Zie [site systeem rollen toevoegen](../deploy/configure/add-site-system-roles.md)voor meer informatie over het plannen van site systemen.

## <a name="plan-for-role-based-administration"></a>Plannen voor op rollen gebaseerd beheer

Beveiliging voor rapportage is vergelijkbaar met andere objecten in Configuration Manager waar u beveiligings rollen en-machtigingen kunt toewijzen aan gebruikers met beheerders rechten. Gebruikers met beheerdersrechten kunnen alleen rapporten uitvoeren en wijzigen waarvoor zij over de toepasselijke beveiligingsrechten beschikken. Als u rapporten wilt uitvoeren in de Configuration Manager-console, moeten gebruikers het **Lees** recht hebben voor de **site** machtiging en de machtigingen die voor specifieke objecten zijn geconfigureerd.

In tegens telling tot andere objecten in Configuration Manager, worden de beveiligings rechten die u instelt voor gebruikers met beheerders bevoegdheden in de Configuration Manager-console ook geconfigureerd in Reporting Services. Wanneer u beveiligings rechten configureert in de Configuration Manager-console, maakt het Reporting Services-punt verbinding met Reporting Services en stelt de juiste machtigingen in voor rapporten.

De beveiligingsrol software- **Update beheer** heeft bijvoorbeeld de machtigingen **rapport uitvoeren** en **rapport wijzigen** . Gebruikers met de rol **Software-update beheer** kunnen alleen rapporten voor software-updates uitvoeren en wijzigen. De Configuration Manager-console geeft geen rapporten weer voor andere objecten aan deze rol. De uitzonde ring hierop is dat sommige rapporten niet aan specifieke Configuration Manager Beveilig bare objecten zijn gekoppeld. De gebruiker met beheerdersrechten moet voor deze rapporten beschikken over het recht **Lezen** voor de machtiging **Site** om de rapporten uit te voeren en de rechten **Wijzigen** voor de machtiging **Site** om de rapporten te wijzigen.  

> [!IMPORTANT]
> Voor gebruikers van een ander domein dan die van het Reporting Services-punt account om rapporten uit te voeren, stelt u een twee richtings relatie in tussen de twee domeinen.

Rapporten zijn volledig ingeschakeld voor op rollen gebaseerd beheer. Configuration Manager de gegevens voor alle opgenomen rapporten worden gefilterd op basis van de machtigingen van de gebruiker die het rapport uitvoert. Gebruikers met specifieke rollen kunnen alleen informatie weer geven die is gedefinieerd voor hun rollen.

Zie [Configure Reporting](configuring-reporting.md)(Engelstalig) voor meer informatie over beveiligings rechten voor rapportage.

Zie op [rollen gebaseerd beheer configureren](../deploy/configure/configure-role-based-administration.md)voor meer informatie over op rollen gebaseerd beheer in Configuration Manager.

## <a name="reporting-recommendations"></a>Aanbevelingen voor rapporten

Houd rekening met de volgende aanbevelingen en tips voor rapportage in Configuration Manager:

- Voor de beste prestaties installeert u het Reporting Services-punt op een extern site systeem. Hoewel u het op de site server kunt installeren, wordt het Reporting Services-punt het beste uitgevoerd wanneer u het op een extern site systeem installeert. Als deze rol achtergrond verwerking heeft, kan deze een concurrentie beding voor systeem bronnen met andere rollen. Er zijn veel variabelen waarmee u rekening moet houden met de prestaties van de site en rol, maar in het algemeen verbetert deze configuratie de rapportage en de algehele prestaties van de site.

- Optimaliseer SQL Server Reporting Services query's. Normaal gesp roken worden rapportage vertragingen veroorzaakt door de tijd die nodig is om query's uit te voeren en de resultaten op te halen. Microsoft SQL Server-hulpprogram ma's zoals Query Analyzer en Profiler kunnen u helpen bij het optimaliseren van query's.

- De verwerking van rapport abonnementen plannen om buiten kantoor uren uit te voeren. Als dat mogelijk is, kan het verwerken van abonnementen buiten kantoor uren de CPU-verwerking op de Configuration Manager site database server minimaliseren. Deze aanbevolen procedure verbetert tevens de beschikbaarheid voor onverwachte rapportaanvragen.

- Met site-updates worden ingebouwde rapporten bewaard. Als u een standaard rapport wijzigt, wordt de naam van het rapport gewijzigd wanneer de site wordt bijgewerkt met een onderstrepings`_`teken (). Dit gedrag zorgt ervoor dat het gewijzigde rapport niet door de site-update wordt overschreven door het standaard rapport.

## <a name="security-and-privacy"></a>Beveiliging en privacy

In Configuration Manager rapporten worden gegevens weer gegeven die worden verzameld tijdens de standaard-Configuration Manager beheer bewerkingen. U kunt bijvoorbeeld een rapport weer geven met informatie die Configuration Manager verzameld van detectie of inventaris. Rapporten kunnen ook de huidige statusinformatie bevatten voor clientbeheeroperaties, zoals implementeren van software en controleren op naleving.

Zie voor meer informatie over aanbevelingen voor beveiliging en privacy-informatie voor Configuration Manager bewerkingen die gegevens kunnen genereren die u in rapporten kunt weer geven, de [beveiliging en privacy voor Configuration Manager](../../plan-design/security/security-and-privacy.md).  

## <a name="next-steps"></a>Volgende stappen

[Vereisten voor rapportage](prerequisites-for-reporting.md)
