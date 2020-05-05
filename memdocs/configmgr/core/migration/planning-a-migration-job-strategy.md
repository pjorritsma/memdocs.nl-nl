---
title: Migratie taak plannen
titleSuffix: Configuration Manager
description: Gebruik migratie taken om gegevens te configureren die u wilt migreren naar uw Configuration Manager huidige branch-omgeving.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a70bfbd4-757a-4468-9312-1c3b373ef9fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87aac20a2ac70e843bf17982375c92804de2b20e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719671"
---
# <a name="plan-a-migration-job-strategy-in-configuration-manager"></a>Een strategie voor een migratie taak plannen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik migratie taken om de specifieke gegevens te configureren die u wilt migreren naar uw Configuration Manager huidige branch-omgeving. Migratie taken identificeren de objecten die u wilt migreren en worden uitgevoerd op de site op het hoogste niveau in uw doel hiërarchie. U kunt een of meer migratie taken per bron site instellen. Hiermee kunt u alle objecten in één keer migreren of met een beperkt aantal subsets van gegevens met elke taak.  

 U kunt migratie taken maken nadat Configuration Manager gegevens van een of meer sites hebt verzameld van de bron hiërarchie. U kunt gegevens in elke volgorde migreren vanaf de bronsites die verzamelde gegevens hebben. Met een Configuration Manager 2007-bron site kunt u alleen gegevens migreren vanaf de site waar een object is gemaakt. Met bron sites waarop System Center 2012 Configuration Manager of hoger wordt uitgevoerd, zijn alle gegevens die u kunt migreren beschikbaar op de site op het hoogste niveau van de bron hiërarchie.  

 Vóór u clients migreert tussen hiërarchieën, moet u ervoor zorgen dat de objecten die clients gebruiken, gemigreerd zijn en dat deze objecten beschikbaar zijn in de doelhiërarchie. Wanneer u bijvoorbeeld migreert vanaf een Configuration Manager 2007 SP2-bron hiërarchie, hebt u mogelijk een aankondiging voor inhoud die is geïmplementeerd naar een aangepaste verzameling die een-client heeft. In dit scenario wordt u aangeraden de verzameling, de advertisement en de bijbehorende inhoud te migreren voordat u de client migreert. Deze gegevens kunnen niet worden gekoppeld aan de client in de doel hiërarchie als de inhoud, verzameling en aankondiging niet worden gemigreerd voordat de client wordt gemigreerd. Indien een client niet gekoppeld is aan de gegevens van een eerder uitgevoerde advertentie en inhoud, kan de client de inhoud aangeboden worden om die te installeren in de doelhiërarchie, wat overbodig kan zijn. Wanneer de client migreert nadat de gegevens zijn gemigreerd, is de client gekoppeld met deze inhoud en advertentie, en, tenzij de advertentie recurrent is, wordt de client deze inhoud voor de gemigreerde advertentie niet meer aangeboden.  

 Sommige objecten vereisen meer dan de migratie van gegevens van de bronhiërarchie naar de doelhiërarchie. Als u bijvoorbeeld software-updates voor uw clients wilt migreren naar uw doel hiërarchie, moet u een actief software-update punt implementeren, de catalogus met producten configureren en het software-update punt synchroniseren met Windows Server Update Services (WSUS) in de doel hiërarchie.  

##  <a name="types-of-migration-jobs"></a><a name="Types_of_Migration"></a>Typen migratie taken  
 Configuration Manager ondersteunt de volgende typen migratie taken. Elk taak type is ontworpen om u te helpen bij het definiëren van de objecten die u in deze taak kunt gebruiken.  

 **Verzamelings migratie** (alleen ondersteund bij het migreren van Configuration Manager 2007 SP2): objecten migreren die gerelateerd zijn aan verzamelingen die u selecteert. Standaard omvat het migreren van verzamelingen alle objecten die zijn gekoppeld aan leden van de verzameling. U kunt specifieke instanties van objecten uitsluiten wanneer u een verzamelingmigratietaak gebruikt.  

 **Object migratie**: Hiermee worden afzonderlijke objecten die u selecteert, gemigreerd. U kunt enkel specifieke gegevens selecteren die u wilt migreren.  

 **Eerder gemigreerde**objecten migreren: gemigreerde objecten die u eerder hebt gemigreerd toen ze zijn bijgewerkt in de bron hiërarchie nadat ze voor het laatst zijn gemigreerd.  

###  <a name="objects-that-you-can-migrate"></a><a name="Objects_that_can_migrate"></a>Objecten die u kunt migreren  
 Niet elk object kan gemigreerd worden door een specifiek type migratietaak. In de volgende lijst staat het type objecten dat u kunt migreren met elk type migratietaak.  

> [!NOTE]  
>  Migratie taken voor verzamelingen zijn alleen beschikbaar wanneer u objecten migreert vanuit een Configuration Manager 2007 SP2-bron hiërarchie.  

 **Taak typen die u kunt gebruiken om elk object te migreren**  

-   **Advertenties** (beschikbaar voor migratie vanaf ondersteunde Configuration Manager 2007-bron sites)  

    -   Verzamelingmigratie  


-   **Asset Intelligence-catalogus**  

    -   Objectmigratie  

    -   Eerder gemigreerde objecten migreren  

-   **Hardwarevereisten Asset Intelligence**  

    -   Objectmigratie  

    -   Eerder gemigreerde objecten migreren  

-   **Softwarelijst Asset Intelligence**  

    -   Objectmigratie  

    -   Eerder gemigreerde objecten migreren  

-   **Grenzen**  

    -   Objectmigratie  

    -   Eerder gemigreerde objecten migreren  

-   **Configuratiebasislijn**  

    -   Verzamelingmigratie  

    -   Objectmigratie  

    -   Eerder gemigreerde objecten migreren  

-   **Configuratie-items**  

    -   Verzamelingmigratie  

    -   Objectmigratie  

    -   Eerder gemigreerde objecten migreren  

-   **Onderhoudsvensters**  

    -   Verzamelingmigratie  


-   **Opstartinstallatiekopieën van besturingssysteem implementeren**  

    -   Verzamelingmigratie  

    -   Objectmigratie  

    -   Eerder gemigreerde objecten migreren  

-   **Stuurprogrammapakketten voor implementatie van besturingssysteem**  

    -   Verzamelingmigratie  

    -   Objectmigratie  

    -   Eerder gemigreerde objecten migreren  

-   **Implementatie van besturingssysteem**  

    -   Verzamelingmigratie  

    -   Objectmigratie  

    -   Eerder gemigreerde objecten migreren  

-   **Installatiekopieën van besturingssysteem implementeren**  

    -   Verzamelingmigratie  

    -   Objectmigratie  

    -   Eerder gemigreerde objecten migreren  

-   **Stuurprogrammapakketten voor implementatie van besturingssysteem**  

    -   Verzamelingmigratie  

    -   Objectmigratie  

    -   Eerder gemigreerde objecten migreren  

-   **Softwaredistributiepakketten**  

    -   Verzamelingmigratie  

    -   Objectmigratie  

    -   Eerder gemigreerde objecten migreren  

-   **Regels voor softwarelicentiecontrole**  

    -   Objectmigratie  

    -   Eerder gemigreerde objecten migreren  

-   **Implementatiepakketten voor software-updates**  

    -   Verzamelingmigratie  

    -   Objectmigratie  

    -   Eerder gemigreerde objecten migreren  

-   **Software-update-implementatiesjablonen**  

    -   Verzamelingmigratie  

    -   Objectmigratie  

    -   Eerder gemigreerde objecten migreren  

-   **Software-update-implementaties**  

    -   Verzamelingmigratie  


-   **Lijsten met software-updates**  

    -   Objectmigratie  

    -   Eerder gemigreerde objecten migreren  

-   **Takenreeksen**  

    -   Verzamelingmigratie  

    -   Objectmigratie  

    -   Eerder gemigreerde objecten migreren  

-   **Virtuele toepassingspakketten**  

    -   Verzamelingmigratie  

    -   Objectmigratie  

    > [!IMPORTANT]  
    >  Hoewel u een virtueel toepassingspakket met objectmigratie kunt migreren, kunt u de pakketten niet migreren met het type migratietaak **Eerder gemigreerde objecten migreren**. In plaats daarvan moet u het gemigreerde virtuele toepassingspakket wissen van de doelsite en dan een nieuwe migratietaak maken om de virtuele toepassing te migreren.  

##  <a name="general-planning-for-all-migration-jobs"></a><a name="About_Migration_Jobs"></a>Algemene planning voor alle migratie taken  
 Gebruik de wizard Migratie taak maken om een migratie taak te maken om objecten te migreren naar uw doel hiërarchie. Het type migratietaak dat u maakt, bepaalt welke objecten beschikbaar zijn voor migratie. U kunt meerdere migratie taken maken en gebruiken om gegevens te migreren van dezelfde bron site of van meerdere bron sites. Het gebruik van één type migratietaak blokkeert het gebruik niet van een ander type migratietaak.  

 Wanneer een migratietaak is uitgevoerd, wordt de status ervan weergegeven als **Voltooid** en kan de taak niet nogmaals worden uitgevoerd. U kunt evenwel een nieuwe migratietaak maken om één van de objecten te migreren die door de oorspronkelijke taak gemigreerd werden, en de nieuwe migratietaak kan ook bijkomende objecten bevatten. Wanneer u aanvullende migratie taken maakt, wordt de status van **gemigreerd**weer gegeven in de objecten die eerder zijn gemigreerd. U kunt deze objecten selecteren om ze opnieuw te migreren, maar tenzij het object is bijgewerkt in de bron hiërarchie, is het niet nodig om deze objecten opnieuw te migreren. Als het object in de bronhiërarchie wordt bijgewerkt nadat het is gemigreerd, kunt u dat object herkennen wanneer u het type migratietaak **Objecten gewijzigd na migratie** gebruikt.  

 U kunt een migratietaak verwijderen voordat deze wordt uitgevoerd. Na het volt ooien van een migratie taak blijft deze echter zichtbaar in de Configuration Manager-console en kan niet worden verwijderd. Elke migratie taak die is voltooid of nog niet is uitgevoerd, blijft zichtbaar in de Configuration Manager-console totdat u het migratie proces voltooit en de migratie gegevens opschoont.  

> [!NOTE]  
>  Nadat u de migratie hebt voltooid met behulp van de actie **migratie gegevens opschonen** , kunt u dezelfde hiërarchie als de huidige bron hiërarchie opnieuw configureren om de zicht baarheid te herstellen van de objecten die u eerder hebt gemigreerd.  

 U kunt de objecten in een migratie taak in de Configuration Manager-console weer geven door de migratie taak te selecteren en vervolgens **op het tabblad objecten in taak** te klikken.  

 Gebruik de informatie in de volgende secties om u te helpen plannen voor migratietaken:  

### <a name="data-selection"></a>Gegevensselectie  
 Wanneer u een verzamelingmigratietaak maakt, moet u één of meerdere verzamelingen selecteren. Nadat u de verzamelingen hebt geselecteerd, worden in de wizard Migratie taak maken de objecten weer gegeven die zijn gekoppeld aan de verzamelingen. Standaard worden alle objecten die zijn gekoppeld aan de geselecteerde verzamelingen gemigreerd, maar u kunt de objecten die u niet met die taak wilt migreren, uitschakelen. Wanneer u een object uitschakelt dat afhankelijke objecten heeft, worden deze afhankelijke objecten ook uitgeschakeld. Alle niet-ingeschakelde objecten worden toegevoegd aan een uitsluitings lijst. Objecten die op een uitsluitingslijst staan, worden verwijderd van automatische selectie voor toekomstige migratietaken. U moet handmatig de uitsluitingslijst bewerken om objecten te verwijderen die u automatisch geselecteerd wenst te zien in migratietaken die u in de toekomst zult maken.  

### <a name="site-ownership-for-migrated-content"></a>Site eigendom voor gemigreerde inhoud  
 Wanneer u inhoud voor implementaties migreert, moet u het inhoudsobject toewijzen aan een site in de doelhiërarchie. Deze site wordt vervolgens de eigenaar van de desbetreffende inhoud in de doelhiërarchie. Hoewel de site op het hoogste niveau van uw doelhiërarchie de site is die de metagegevens voor inhoud feitelijk migreert, is het de toegewezen site die de oorspronkelijke bronbestanden voor de inhoud via het netwerk benadert.  

 Overweeg om eigendom van inhoud over te dragen naar de dichtsbijgelegen site, om de netwerkbandbreedte te minimaliseren die gebruikt wordt tijdens migratie, Omdat informatie over de inhoud globaal wordt gedeeld in Configuration Manager, is deze beschikbaar op elke site.  

 Informatie over inhoud wordt gedeeld met alle sites in de doel hiërarchie met behulp van database replicatie. Alle inhoud die u toewijst aan een primaire site en vervolgens implementeert naar distributie punten op andere primaire sites, wordt echter door gebruik te maken van replicatie op basis van een bestand. De overdracht wordt doorgestuurd via de centrale beheersite en dan naar elke bijkomende primaire site. Door het centraliseren van pakketten die u voor of tijdens de migratie naar meerdere primaire sites wilt distribueren wanneer u een site toewijst als eigenaar van de inhoud, kunt u gegevens overdrachten over netwerken met een lage band breedte reduceren.  

### <a name="role-based-administration-security-scopes-for-migrated-data"></a>Beveiligingsbereiken voor beheer op basis van rollen voor gemigreerde gegevens  
 Wanneer u gegevens migreert naar een doel hiërarchie, moet u een of meer op rollen gebaseerd beheer beveiligingsbereiken toewijzen aan de objecten waarvan de gegevens worden gemigreerd. Dit waarborgt dat enkel de geschikte gebruikers met beheerdersrechten toegang hebben tot deze gegevens nadat ze gemigreerd zijn. De beveiligingsbereiken die u specificeert zijn gedefinieerd door de migratietaak en zijn toegepast voor elk object dat gemigreerd is door deze taak. Als u wilt dat verschillende beveiligingsbereiken worden toegepast op verschillende sets objecten en u deze bereiken tijdens de migratie wilt toewijzen, moet u de verschillende sets objecten migreren door verschillende migratie taken te gebruiken.  

 Controleer voordat u een migratie taak instelt hoe beheer op basis van rollen werkt in Configuration Manager. Stel, indien nodig, een of meer beveiligingsbereiken in voor de gegevens die u migreert om te bepalen wie toegang heeft tot de gemigreerde objecten in de doel hiërarchie.  

 Zie [basis principes van op rollen gebaseerd beheer voor Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md)voor meer informatie over beveiligingsbereiken en beheer op basis van rollen.  

### <a name="review-migration-actions"></a>Migratieacties controleren  
 Wanneer u een migratie taak instelt, wordt in de wizard Migratie taak maken een lijst weer gegeven met de acties die u moet uitvoeren om ervoor te zorgen dat een geslaagde migratie en een lijst met acties die Configuration Manager ondernemen tijdens de migratie van de geselecteerde gegevens. Bekijk deze informatie zorgvuldig om het verwachte resultaat te controleren.  

### <a name="schedule-migration-jobs"></a>Migratie taken plannen  
 Standaard wordt een migratietaak uitgevoerd onmiddellijk nadat hij werd gemaakt. U kunt echter opgeven wanneer de migratie taak wordt uitgevoerd wanneer u de taak maakt of door de eigenschappen van de taak te bewerken. U kunt plannen dat de migratie taak als volgt wordt uitgevoerd:  

-   Taak nu uitvoeren  

-   Voer de taak op een specifiek begin-tijdstip uit  

-   De taak niet uitvoeren  

### <a name="specify-conflict-resolution-for-migrated-data"></a>Conflictoplossing opgeven voor gemigreerde gegevens  
 Standaard overschrijven migratie taken geen gegevens in de doel database, tenzij u de migratie taak configureert om gegevens over te slaan of te overschrijven die eerder naar de doel database zijn gemigreerd.  

##  <a name="plan-for-collection-migration-jobs"></a><a name="About_Collection_Migration"></a>Planning voor verzamelings migratie taken  
 Migratie taken voor verzamelingen zijn alleen beschikbaar wanneer u gegevens migreert vanaf een bron hiërarchie waarop een ondersteunde versie van Configuration Manager 2007 wordt uitgevoerd. Wanneer u per verzameling migreert, moet u een of meer verzamelingen opgeven die u wilt migreren. Voor elke verzameling die u opgeeft, selecteert de migratietaak automatisch alle verwante objecten voor migratie. Als u bijvoorbeeld een specifieke verzameling gebruikers selecteert, worden vervolgens de leden van de verzameling vastgesteld, waarna u de implementatie met betrekking tot die verzameling kunt migreren. U kunt voor de migratie eventueel andere implementatie-objecten selecteren die verband houden met die leden. Al deze geselecteerde items worden aan de lijst van de te migreren objecten toegevoegd.  

 Wanneer u een verzameling migreert, worden door Configuration Manager ook verzamelings instellingen gemigreerd, met inbegrip van onderhouds Vensters en verzamelings variabelen, maar kan de verzamelings instellingen voor AMT-client inrichting niet worden gemigreerd.  

 Gebruik de informatie in de volgende gedeelten voor meer informatie over aanvullende configuraties die kunnen worden toegepast op migratie taken op basis van verzamelingen.  

### <a name="exclude-objects-from-collection-migration-jobs"></a>Objecten uitsluiten van verzamelings migratie taken  
 U kunt specifieke objecten uitsluiten van een verzamelingmigratietaak. Wanneer u een specifiek object uitsluit van een migratie taak voor een verzameling, wordt dat object toegevoegd aan een globale uitsluitings lijst met alle objecten die u hebt uitgesloten van migratie taken die voor een bron site in de huidige bron hiërarchie zijn gemaakt. Objecten op de uitsluitings lijst zijn nog steeds beschikbaar voor migratie in toekomstige taken, maar worden niet automatisch opgenomen wanneer u een nieuwe migratie taak op basis van verzamelingen maakt.  

 U kunt de uitsluitingslijst zo bewerken, dat objecten die u eerder hebt uitgesloten, worden verwijderd. Wanneer u een object van de uitsluitingslijst hebt verwijderd, wordt deze vervolgens automatisch geselecteerd wanneer een verwante verzameling tijdens het maken van een nieuwe migratietaak wordt opgegeven.  

### <a name="unsupported-collections"></a>Niet-ondersteunde verzamelingen  
 Configuration Manager kunt een van de standaard gebruikers verzamelingen, Apparaatsets en de meeste aangepaste verzamelingen migreren uit een Configuration Manager 2007-bron hiërarchie. Configuration Manager kan echter geen verzamelingen migreren die gebruikers en apparaten bevatten in dezelfde verzameling.  

 De volgende verzamelingen kunnen niet worden gemigreerd:  

-   Een verzameling die gebruikers en apparaten heeft.  

-   Een verzameling die een verwijzing bevat naar een verzameling van een verschillend resource type. Bijvoorbeeld een verzameling op basis van een apparaat met een subverzameling of een koppeling naar een verzameling op basis van een gebruiker. In dit voor beeld wordt alleen de verzameling op het hoogste niveau gemigreerd.  

-   Een verzameling met een regel die onbekende computers bevat. De verzameling wordt gemigreerd, maar de regel die onbekende computers bijvoegt niet.  

### <a name="empty-collections"></a>Lege verzamelingen  
 Een lege verzameling is een verzameling waaraan geen resources zijn gekoppeld. Wanneer Configuration Manager een lege verzameling migreert, wordt de verzameling geconverteerd naar een organisatorische map die geen gebruikers of apparaten heeft. Deze map wordt gemaakt met de naam van de lege verzameling onder het knoop punt **gebruikers verzamelingen** of **apparaat verzamelingen** in de werk ruimte **activa en naleving** in de Configuration Manager-console.  

### <a name="linked-collections-and-subcollections"></a>Gekoppelde verzamelingen en subverzamelingen  
 Wanneer u verzamelingen migreert die zijn gekoppeld aan andere verzamelingen of die subverzamelingen hebben, maakt Configuration Manager naast de gekoppelde verzamelingen en subverzamelingen een map onder het knoop punt **gebruikers verzamelingen** of **apparaat** .  

### <a name="collection-dependencies-and-include-objects"></a>Verzamelingafhankelijkheden en objecten opnemen  
 Wanneer u een verzameling opgeeft die u in de wizard Migratie taak maken wilt migreren, worden alle afhankelijke verzamelingen automatisch geselecteerd om in de taak te worden opgenomen. Dit gedrag zorgt ervoor dat alle benodigde resources na de migratie beschikbaar zijn.  

 Bijvoorbeeld: u selecteert een verzameling voor apparaten met Windows 10 en krijgt de naam **Win_10**. Deze verzameling is beperkt tot een verzameling met al uw client besturingssystemen en heeft de naam **All_Clients**. De verzameling **All_Clients** wordt automatisch geselecteerd voor migratie.  

### <a name="collection-limiting"></a>Beperkende verzameling  
 Met Configuration Manager current branch zijn verzamelingen globale gegevens en worden ze geëvalueerd op elke site in de hiërarchie. Plan daarom hoe u het bereik van een verzameling wilt beperken nadat deze is gemigreerd. U kunt tijdens de migratie een verzameling uit de te gebruiken doelhiërarchie aanduiden om het bereik van de door u gemigreerde verzameling te beperken, zodat de gemigreerde verzameling geen onverwachte leden bevat.  

 In Configuration Manager 2007 worden verzamelingen bijvoorbeeld geëvalueerd op de site die ze maakt en op onderliggende sites. Er wordt misschien alleen een aankondiging naar een onderliggende site geïmplementeerd, hetgeen het bereik voor die aankondiging zou beperken tot die onderliggende site. Ten opzichte van Configuration Manager current branch worden verzamelingen geëvalueerd op elke site en worden de bijbehorende advertenties geëvalueerd voor elke site. U kunt met Beperkende verzameling de verzamelingsleden filteren op basis van een andere verzameling, om te voorkomen dat er onverwachte verzamelingsleden worden toegevoegd.  

### <a name="site-code-replacement"></a>Sitecode vervangen  
 Wanneer u een verzameling migreert die criteria bevat die een Configuration Manager 2007-site aanduiden, moet u een specifieke site opgeven in de doel hiërarchie. Hiermee zorgt u ervoor dat de gemigreerde verzameling blijft werken in uw doelhiërarchie en het bereik ervan niet groter wordt.  

### <a name="specify-behavior-for-migrated-advertisements"></a>Gedrag voor gemigreerde advertenties opgeven  
 Migratie taken op basis van verzamelingen uitschakelen standaard advertisements die naar de doel hiërarchie migreren. Dit omvat alle programma's die aan de aankondiging gekoppeld zijn. Wanneer u een migratie taak op basis van verzamelingen maakt die aankondigingen bevat, ziet u de optie **Program ma's voor implementatie inschakelen in Configuration Manager nadat een aankondiging is gemigreerd** op de pagina **instellingen** van de wizard Migratie taak maken. Als u deze optie selecteert, worden programma's ingeschakeld die aan de aankondigingen zijn gekoppeld na hun migratie. Selecteer deze optie niet als best practice. Schakel in plaats daarvan de Program ma's in nadat deze zijn gemigreerd wanneer u de clients die deze zullen ontvangen, kunt controleren.  

> [!NOTE]  
>  U ziet de optie **Program ma's voor implementatie inschakelen in Configuration Manager nadat een aankondiging is gemigreerd** alleen wanneer u een migratie taak op basis van verzamelingen maakt en de migratie taak aankondigingen bevat.  

 Als u een programma na migratie wilt inschakelen, schakelt u **dit programma uitschakelen uit op computers waarop het wordt geadverteerd** op het tabblad **Geavanceerd** van de programma-eigenschappen.  

##  <a name="plan-for-object-migration-jobs"></a><a name="About_Object_Migration"></a>Plannen voor object migratie taken  
 In tegenstelling tot verzamelingmigratie moet u elk object en objectinstantie selecteren dat/die u wilt migreren. U kunt de afzonderlijke objecten (zoals advertenties van een Configuration Manager 2007-hiërarchie of een publicatie van een System Center 2012 Configuration Manager of Configuration Manager huidige branch-hiërarchie) selecteren om toe te voegen aan de lijst met objecten die moeten worden gemigreerd voor een specifieke migratie taak. Objecten die u niet aan de migratielijst toevoegt, worden niet door de objectmigratietaak naar de doelsite gemigreerd.  

 Migratie taken op basis van objecten bevatten geen aanvullende configuraties die van toepassing zijn op alle migratie taken.  

##  <a name="plan-for-previously-migrated-object-migration-jobs"></a><a name="About_Object_Migrations"></a>Plannen voor eerder gemigreerde object migratie taken  
 Wanneer een object dat u al naar de doelhiërarchie hebt gemigreerd, wordt bijgewerkt in de bronhiërarchie, kunt u dat object opnieuw migreren met het taaktype **Objecten gewijzigd na migratie**. Wanneer u bijvoorbeeld de bron bestanden voor een pakket in de bron hiërarchie hernoemt of bijwerkt, wordt de pakket versie verhoogd in de bron hiërarchie. Wanneer de pakketversie stapsgewijs is verhoogd, kan het pakket door dit taaktype worden aangeduid voor migratie.  

 Dit taaktype is gelijk aan het objectmigratietype, behalve dat wanneer u objecten selecteert die u wilt migreren, u alleen een selectie kunt maken uit objecten die zijn bijgewerkt nadat deze zijn gemigreerd door een eerdere migratietaak.   

 Wanneer u dit taak type selecteert, wordt het gedrag voor conflict oplossing op de pagina **instellingen** van de wizard Migratie taak maken geconfigureerd om eerder gemigreerde objecten te overschrijven. Deze instelling kan niet worden gewijzigd.  

> [!NOTE]  
>  Deze migratietaak kan objecten aanduiden die automaisch worden bijgewerkt door de bronhiërarchie, en objecten die door een gebruiker met beheerdersrechten worden bijgewerkt.  
