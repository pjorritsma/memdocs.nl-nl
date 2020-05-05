---
title: Grond beginselen van op rollen gebaseerd beheer
titleSuffix: Configuration Manager
description: Gebruik op rollen gebaseerd beheer om beheerders toegang te beheren tot Configuration Manager en objecten die u beheert.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0a2d6c3f-a4e4-4c19-b087-3caada480de9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 62faf2fd736f9751e8b33e821cb814f527a1197c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722856"
---
# <a name="fundamentals-of-role-based-administration-for-configuration-manager"></a>Basis principes van beheer op basis van rollen voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met Configuration Manager gebruikt u beheer op basis van rollen om de toegang te beveiligen die nodig is voor het beheren van Configuration Manager. U beveiligt ook de toegang tot de objecten die u beheert, zoals verzamelingen, implementaties en sites. Nadat u de concepten hebt gemaakt die in dit artikel zijn geïntroduceerd, kunt u [op rollen gebaseerd beheer configureren voor Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

 Het op rollen gebaseerde beheer model definieert en beheert centraal instellingen voor beveiligings toegang voor alle sites en site-instellingen met behulp van de volgende items:  

- *Beveiligings rollen* worden toegewezen aan gebruikers met beheerders rechten om die gebruikers (of groepen gebruikers) toestemming te geven voor verschillende Configuration Manager-objecten. Bijvoorbeeld machtiging voor het maken of wijzigen van client instellingen.  

- *Beveiligingsbereiken* worden gebruikt voor het groeperen van specifieke exemplaren van objecten die een gebruiker met beheerders rechten moet beheren, zoals een toepassing die Microsoft Office 2010 installeert.  

- *Verzamelingen* worden gebruikt om groepen gebruikers-en apparaat bronnen op te geven die door de gebruiker met beheerders rechten kunnen worden beheerd.  

  Met de combi natie van beveiligings rollen, beveiligingsbereiken en verzamelingen, scheidt u de beheer toewijzingen die voldoen aan de vereisten van uw organisatie. Samen worden gebruikt, wordt het beheer bereik van een gebruiker gedefinieerd, wat de gebruiker kan bekijken en beheren in uw Configuration Manager-implementatie.  

## <a name="benefits-of-role-based-administration"></a>Voor delen van beheer op basis van rollen  

- Sites worden niet gebruikt als beheer grenzen.  
- U maakt gebruikers met beheerders rechten voor een hiërarchie en hoeft alleen maar één keer beveiliging toe te wijzen.  
- Alle beveiligings toewijzingen worden gerepliceerd en zijn beschikbaar in de hele hiërarchie.  
- Er zijn ingebouwde beveiligings rollen die worden gebruikt om de typische beheer taken toe te wijzen. Maak uw eigen aangepaste beveiligings rollen ter ondersteuning van uw specifieke bedrijfs vereisten.  
- Gebruikers met beheerders rechten zien alleen de objecten waarvoor ze machtigingen hebben om ze te beheren.  
- U kunt acties administratieve beveiliging controleren.  

Wanneer u administratieve beveiliging ontwerpt en implementeert voor Configuration Manager, kunt u het volgende gebruiken om een *beheer bereik* voor een gebruiker met beheerders rechten te maken:  

- [Beveiligings rollen](#bkmk_Planroles)  

- [Verzamelingen](#bkmk_planCol)  

- [Beveiligingsbereiken](#bkmk_PlanScope)  

 Het beheer bereik bepaalt de objecten die een gebruiker met beheerders rechten bekijkt in de Configuration Manager-console en de machtigingen die een gebruiker heeft voor deze objecten. De configuraties voor rolgebaseerd beheer worden op elke site in de hiërarchie gerepliceerd als globale gegevens, en vervolgens toegepast op alle beheerverbindingen.  

> [!IMPORTANT]  
> Door vertragingen in de replicatie van de ene site naar de andere is het mogelijk dat een site geen wijzigingen ontvangt voor rolgebaseerd beheer. Zie het onderwerp [gegevens overdracht tussen sites](../plan-design/hierarchy/data-transfers-between-sites.md) voor meer informatie over het controleren van de replicatie van de intersite-data base.  

##  <a name="security-roles"></a><a name="bkmk_Planroles"></a>Beveiligings rollen

 Gebruik beveiligingsrollen voor het verlenen van beveiligingsmachtigingen aan gebruikers met beheerdersrechten. Beveiligingsrollen zijn groepen van beveiligingsmachtigingen die u toekent aan gebruikers met beheerdersrechten zodat zij hun beheertaken kunnen uitvoeren. Deze beveiligingsmachtigingen bepalen de beheeracties die een gebruiker met beheerdersrechten kan uitvoeren en de machtigingen die voor bepaalde objecttypes worden verleend. Aanbevolen wordt om de beveiligingsrollen toe te kennen waaraan de minste machtigingen zijn verbonden.  

 Configuration Manager heeft verschillende ingebouwde beveiligings rollen ter ondersteuning van typische groeperingen van beheer taken, en u kunt uw eigen aangepaste beveiligings rollen maken ter ondersteuning van uw specifieke bedrijfs vereisten. Voorbeelden van ingebouwde beveiligingsrollen:  

- *Volledige beheerder* verleent alle machtigingen in Configuration Manager.  

- *Asset Manager* verleent machtigingen voor het beheren van het Asset Intelligence synchronisatie punt, Asset Intelligence rapportage klassen, software-inventaris, hardware-inventaris en meet regels.  

- *Software-update beheer* verleent machtigingen voor het definiëren en implementeren van software-updates. Gebruikers met beheerders rechten die aan deze rol zijn gekoppeld, kunnen verzamelingen, software-update groepen, implementaties en sjablonen maken.  

- De *beveiligings beheerder* verleent machtigingen voor het toevoegen en verwijderen van gebruikers met beheerders rechten en het koppelen van administratieve gebruikers met beveiligings rollen, verzamelingen en beveiligingsbereiken. Gebruikers met beheerders rechten die aan deze rol zijn gekoppeld, kunnen ook beveiligings rollen en hun toegewezen beveiligingsbereiken en verzamelingen maken, wijzigen en verwijderen.

> [!TIP]  
> U kunt de lijst met ingebouwde beveiligings rollen en aangepaste beveiligings rollen die u maakt, met inbegrip van de bijbehorende beschrijvingen, bekijken in de Configuration Manager-console. Als u de rollen wilt weer geven, vouwt u in de werk ruimte **beheer** de optie **beveiliging**uit en selecteert u **beveiligings rollen**.  

 Elke beveiligingsrol heeft specifieke machtigingen voor verschillende objecttypen. De beveiligingsrol *toepassings Auteur* heeft bijvoorbeeld de volgende machtigingen voor toepassingen: goed keuren, maken, verwijderen, wijzigen, map wijzigen, object verplaatsen, lezen, rapport uitvoeren en beveiligings bereik instellen.

 U kunt de machtigingen voor de ingebouwde beveiligings rollen niet wijzigen, maar het is wel mogelijk om de rol te kopiëren, wijzigingen aan te brengen en deze wijzigingen vervolgens op te slaan als een nieuwe aangepaste beveiligingsrol. U kunt ook beveiligings rollen importeren die u hebt geëxporteerd uit een andere hiërarchie, bijvoorbeeld van een test netwerk. Bekijk de beveiligings rollen en de bijbehorende machtigingen om te bepalen of u de ingebouwde beveiligings rollen gaat gebruiken of dat u uw eigen aangepaste beveiligings rollen moet maken.  

### <a name="to-help-you-plan-for-security-roles"></a>Om u te helpen bij het plannen van beveiligings rollen  

1. Identificeer de taken die de gebruikers met beheerders rechten uitvoeren in Configuration Manager. Deze rollen kunnen betrekking hebben op één of meer groepen van beheertaken, zoals implementatie van toepassingen en pakketten, implementatie van besturingssystemen en instellingen voor naleving, controle, externe bediening van computers, en verzameling van inventarisgegevens.  

2. Wijs deze administratieve taken toe aan één of meer van de ingebouwde beveiligingsrollen.  

3. Als sommige gebruikers met beheerders rechten de taken van meerdere beveiligings rollen uitvoeren, wijst u de meerdere beveiligings rollen toe aan deze gebruikers met beheerders rechten in plaats van een nieuwe beveiligingsrol te maken die de taken combineert.  

4. Als de taken die u hebt geïdentificeerd niet zijn toegewezen aan de ingebouwde beveiligings rollen, maakt en test u nieuwe beveiligings rollen.  

Voor informatie over het maken en configureren van beveiligings rollen voor beheer op basis van rollen, Zie [aangepaste beveiligings rollen maken](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole) en [beveiligings rollen configureren](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole) in het artikel [beheer op basis van rollen configureren voor Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md) .  

##  <a name="collections"></a><a name="bkmk_planCol"></a>Reeksen

 Verzamelingen specificeren de gebruiker en computerbronnen die een gebruiker met beheerdersrechten kan bekijken of beheren. Bijvoorbeeld, als een gebruiker met beheerdersrechten toepassingen wil kunnen implementeren of een computer extern wil kunnen bedienen, moet er een beveiligingsrol aan hem zijn toegewezen die hem toegang verleent tot een verzameling die deze bronnen bevat. U kunt verzamelingen van gebruikers of apparaten selecteren.  

 Zie [Inleiding tot verzamelingen](../../core/clients/manage/collections/introduction-to-collections.md)voor meer informatie over verzamelingen.  

 Controleer, voordat u rolgebaseerd beheer gaat configureren, of u nieuwe verzamelingen moet maken om een van de volgende redenen:  

- Functionele organisatie. Bijvoorbeeld: afzonderlijke verzamelingen van servers en werkstations.  
- Geografische uitlijning. Bijvoorbeeld: afzonderlijke verzamelingen voor Noord-Amerika en Europa.  
- Beveiligingvereisten en bedrijfsprocessen. Bijvoorbeeld: afzonderlijke verzamelingen voor productie en testcomputers.  
- Uitlijning per organisatie. Bijvoorbeeld, afzonderlijke verzamelingen voor elk bedrijfsonderdeel.  

Voor informatie over het configureren van verzamelingen voor op rollen gebaseerd beheer, Zie [verzamelingen configureren](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl) voor het beheren van beveiliging in het artikel [beheer op basis van rollen configureren voor Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md) .  

## <a name="security-scopes"></a><a name="bkmk_PlanScope"></a>Beveiligingsbereiken

 Gebruik beveiligingsrollen om gebruikers met beheerdersrechten toegang te geven tot beveiligbare objecten. Een beveiligings bereik is een benoemde set Beveilig bare objecten die zijn toegewezen aan gebruikers met beheerders rechten als groep. Alle beveiligbare objecten moeten aan één of meer beveiligingsbereiken zijn toegewezen. Configuration Manager heeft twee ingebouwde beveiligingsbereiken:  

- Het *ingebouwde* beveiligings bereik biedt toegang tot alle bereiken. U kunt geen objecten toewijzen aan dit beveiligings bereik.  

- Het *standaard* ingebouwde beveiligings bereik wordt standaard voor alle objecten gebruikt. Wanneer u Configuration Manager voor het eerst installeert, worden alle objecten aan dit beveiligings bereik toegewezen.  

Als u de objecten die gebruikers met beheerdersrechten kunnen zien en beheren wilt beperken, moet u uw eigen aangepaste beveiligingsbereiken maken en gebruiken. Beveiligingsbereiken bieden geen ondersteuning voor een hiërarchische structuur en kunnen niet worden genest. Beveiligingsbereiken kunnen een of meer object typen bevatten, waaronder de volgende items:  

- Waarschuwingsabonnementen  
- Toepassingen  
- Installatiekopieën  
- Grensgroepen  
- Configuratie-items  
- Aangepaste clientinstellingen  
- Distributiepunten en distributiepuntengroepen  
- Driverpakketten
- Mappen (vanaf versie 1906) <!--3600867-->
- Globale voorwaarden  
- Migratietaken
- Installatiekopieën van besturingssysteem
- Installatiepakketten besturingssysteem  
- Pakketten  
- Query's  
- Sites  
- Regels voor softwarelicentiecontrole  
- Software-updategroepen  
- Software-updatepakketten  
- Takenreekspakketten  
- Windows CE apparaatinstellingsitems en pakketten  

Er zijn ook enkele objecten die u niet in beveiligingsbereiken kunt gebruiken omdat ze alleen worden beveiligd door beveiligings rollen. Beheerders toegang tot deze objecten kan niet worden beperkt tot een subset van de beschik bare objecten. Bijvoorbeeld, u heeft een gebruiker met beheerdersrechten die grensgroepen maakt welke gebruikt worden voor een specifieke site. Omdat het grens object geen beveiligingsbereiken ondersteunt, kunt u deze gebruiker geen beveiligings bereik toewijzen dat toegang geeft tot alleen de grenzen die aan die site kunnen worden gekoppeld. Een grens object kan niet worden gekoppeld aan een beveiligings bereik, wanneer u een beveiligingsrol die toegang heeft tot grens objecten aan een gebruiker toewijst, de gebruiker toegang heeft tot elke grens in de hiërarchie.  

Objecten die niet zijn beperkt door beveiligingsbereiken zijn de volgende items:  

- Active Directory-forests  
- Gebruikers met beheerdersrechten  
- Waarschuwingen  
- Antimalwarebeleid  
- Grenzen  
- Computerkoppelingen  
- Standaardclientinstellingen  
- Implementatiesjablonen  
- Apparaatstuurprogramma 's  
- Exchange Server-connector  
- Toewijzingen tussen sites van migratie  
- Inschrijvingsprofielen voor mobiele apparaten  
- Beveiligingsrollen  
- Beveiligingsbereiken  
- Siteadressen  
- Sitesysteemrollen  
- Softwaretitels  
- Software-updates  
- Statusberichten  
- Gebruikersaffiniteiten apparaat  

Maak beveiligingsbereiken wanneer u toegang tot afzonderlijke instanties van objecten wilt beperken. Bijvoorbeeld:  

- U hebt een groep van gebruikers met beheerdersrechten die productietoepassingen moeten kunnen zien en geen testtoepassingen. Maak één beveiligingsbereik voor productietoepassingen en nog één voor de testtoepassingen.  

- Gebruikers met verschillende beheerdersrechten hebben verschillende toegangsrechten nodig voor bepaalde instanties van een objecttype. Bijvoorbeeld: de ene groep gebruikers met beheerdersrechten heeft de machtiging Lezen nodig voor specifieke software-updategroepen, en een andere groep gebruikers met beheerdersrechten heeft de machtigingen Wijzigen en Verwijderen nodig voor andere software-updategroepen. Maak verschillende beveiligingsbereiken voor deze software-updategroepen.  

Voor informatie over het configureren van beveiligingsbereiken voor beheer op basis van rollen, zie de beveiligingsbereiken configureren [voor een object](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope) in het artikel beheer op [basis van rollen configureren voor Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md) .  

## <a name="next-steps"></a>Volgende stappen

[Op rollen gebaseerd beheer configureren voor Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
