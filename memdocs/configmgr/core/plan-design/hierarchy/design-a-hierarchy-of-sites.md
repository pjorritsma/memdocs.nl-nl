---
title: Een site hiërarchie ontwerpen
titleSuffix: Configuration Manager
description: Inzicht in de beschik bare topologieën en beheer opties voor Configuration Manager om uw site hiërarchie te plannen.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e14cf57e962d7bc90cc39db9ecfea68d9c5b00e
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073344"
---
# <a name="design-a-hierarchy-of-sites-for-configuration-manager"></a>Een hiërarchie van sites ontwerpen voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voordat u de eerste site van een nieuwe Configuration Manager-hiërarchie installeert, is het een goed idee om te begrijpen:  

- De beschik bare topologieën voor Configuration Manager  

- De typen beschik bare sites en hun relatie met elkaar  

- De reik wijdte van het beheer van elk type site  

- De opties voor inhouds beheer waarmee u het aantal sites kunt verminderen dat u moet installeren  

Plan vervolgens een topologie die efficiënt uw huidige bedrijfs behoeften vervult en kan later worden uitgebreid om toekomstige groei te beheren.  

Houd bij het plannen de beperkingen in acht voor het toevoegen van extra sites aan een hiërarchie of een zelfstandige site:  

- Installeer een nieuwe primaire site onder een centrale beheer site tot het [ondersteunde aantal primaire sites](../configs/size-and-scale-numbers.md) voor de hiërarchie.  

- [Vouw een zelfstandige primaire site uit om een nieuwe centrale beheer site te installeren](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand), zodat u extra primaire sites kunt installeren.  

- Nieuwe secundaire sites installeren onder een primaire site, tot de [ondersteunde limiet voor de primaire site en de](../configs/size-and-scale-numbers.md) algehele hiërarchie.  

- U kunt geen eerder geïnstalleerde site toevoegen aan een bestaande hiërarchie om twee zelfstandige sites samen te voegen. Configuration Manager ondersteunt alleen de installatie van nieuwe sites voor een bestaande site hiërarchie.  


> [!NOTE]  
> Wanneer u een nieuwe installatie van Configuration Manager wilt plannen, moet u rekening houden met de opmerkingen bij de [release](../../servers/deploy/install/release-notes.md), die actuele problemen in de actieve versies beschrijven. De release opmerkingen zijn van toepassing op alle vertakkingen van Configuration Manager. Wanneer u de [technische preview-vertakking](../../get-started/technical-preview.md)gebruikt, zoekt u problemen die specifiek zijn voor die vertakking in de documentatie voor elke versie van de Technical Preview.  



##  <a name="hierarchy-topology"></a><a name="bkmk_topology"></a>Hiërarchie topologie  

Hiërarchie topologieën variëren van:  

- Eenvoudigste: Eén zelfstandige primaire site  

- Meest complex: een groep met verbonden primaire en secundaire sites met een centrale beheer site op de site op het hoogste niveau van de hiërarchie  

Het sleutel stuur programma van het type en aantal sites dat u in een hiërarchie gebruikt, is gewoonlijk het aantal en type apparaten dat u moet ondersteunen.   

### <a name="standalone-primary-site"></a>Zelfstandige primaire site

Gebruik een zelfstandige primaire site wanneer het beheer van alle apparaten en gebruikers kan ondersteunen. Zie [grootte en schaal getallen](../configs/size-and-scale-numbers.md)voor meer informatie. Deze topologie slaagt ook wanneer de geografische locaties van uw bedrijf kunnen worden bediend door één primaire site. Gebruik meerdere beheer punten in grens groepen en een zorgvuldig geplande inhouds infrastructuur om netwerk verkeer te beheren. Zie [grens groepen](../../servers/deploy/configure/boundary-groups.md) en [basis concepten voor inhouds beheer](fundamental-concepts-for-content-management.md)configureren voor meer informatie.  

Deze topologie biedt de volgende voor delen:  

- Eenvoudigere administratieve overhead  

- Vereenvoudigde clientsitetoewijzing en detectie van beschikbare resources en services  

- Eliminatie van mogelijke vertragingen die worden geïntroduceerd door database replicatie tussen sites  

- Optie voor het uitbreiden van een zelfstandige primaire site in een grotere hiërarchie met een centrale beheer site. Met deze optie kunt u vervolgens nieuwe primaire sites installeren om de schaal van uw implementatie uit te breiden.  


### <a name="central-administration-site-with-one-or-more-child-primary-sites"></a>Centrale beheer site met een of meer onderliggende primaire sites 

Gebruik deze topologie als u meer dan één primaire site nodig hebt om het beheer van al uw apparaten en gebruikers te ondersteunen. Dit is vereist wanneer u meer dan één primaire site moet gebruiken. 

Deze topologie biedt de volgende voor delen:  

- Het ondersteunt Maxi maal 25 primaire sites waarmee u de schaal van uw hiërarchie kunt uitbreiden.    

- U gebruikt altijd de centrale beheer site, tenzij u uw sites opnieuw installeert. Deze optie is permanent. U kunt een onderliggende primaire site niet loskoppelen om er een zelfstandige primaire site van te maken.  



##  <a name="determine-when-to-use-a-central-administration-site"></a><a name="BKMK_ChooseCAS"></a>Bepalen wanneer u een centrale beheer site wilt gebruiken  

Gebruik een centrale beheer site om instellingen voor de gehele hiërarchie te configureren en om alle sites en objecten in de hiërarchie te bewaken. Dit site type beheert clients niet rechtstreeks. Het coördineert site-naar-site gegevens replicatie, met daarin de configuratie van sites en clients in de hiërarchie.  

De volgende informatie helpt u te bepalen wanneer u een centrale beheersite installeert:  

- De centrale beheer site is de site op het hoogste niveau in een hiërarchie.  

- Wanneer u een hiërarchie configureert die meer dan één primaire site heeft, installeert u een centrale beheer site.  

     - Als u onmiddellijk twee of meer primaire sites nodig hebt, moet u eerst de centrale beheer site installeren.  

     - Als u al een primaire site hebt en vervolgens een centrale beheer site wilt installeren, [vouwt u de zelfstandige primaire site uit](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand) om de centrale beheer site te installeren.  

- De centrale beheer site ondersteunt alleen primaire sites als onderliggende sites.  

- Aan de centrale beheer site kunnen geen clients worden toegewezen.  

- De centrale beheer site biedt geen ondersteuning voor site systeem rollen die rechtstreeks ondersteuning bieden voor clients, zoals beheer punten en distributie punten.  

- Alle clients in de hiërarchie beheren en alle site beheer taken uitvoeren vanuit de Configuration Manager-console die is verbonden met de centrale beheer site. Deze taken omvatten het installeren van beheer punten of andere site systeem rollen op onderliggende primaire of secundaire sites.  

- Wanneer u een centrale beheer site gebruikt, is dit de enige plaats waar u site gegevens van alle sites in uw hiërarchie ziet. Deze gegevens omvatten informatie zoals inventaris gegevens en status berichten.  

- Configureer detectie bewerkingen in de gehele hiërarchie vanaf de centrale beheer site. Wijs op de centrale beheer site detectie methoden toe om uit te voeren op afzonderlijke primaire sites.  

- Beveiliging beheren in de gehele hiërarchie door verschillende beveiligings rollen, beveiligingsbereiken en verzamelingen toe te wijzen aan verschillende gebruikers met beheerders rechten. Deze configuraties zijn van toepassing op elke site in de hiërarchie.  

- Configureer replicatie om de communicatie tussen sites in de hiërarchie te beheren. Planning van database replicatie voor site gegevens en het beheren van de band breedte voor de overdracht van op bestanden gebaseerde gegevens tussen sites.  



##  <a name="determine-when-to-use-a-primary-site"></a><a name="BKMK_ChoosePriimary"></a>Bepalen wanneer een primaire site moet worden gebruikt  

Gebruik primaire sites om clients te beheren. Een primaire site installeren als een onderliggende site onder een centrale beheer site, of als de eerste site van een nieuwe hiërarchie. Een primaire site die de eerste site van een hiërarchie is, maakt een zelfstandige primaire site. Zowel onderliggende primaire sites als zelfstandige primaire sites ondersteunen secundaire sites.  

Overweeg om de volgende redenen extra primaire sites toe te voegen:  

- Als u het aantal apparaten wilt verhogen, beheert u met één hiërarchie.  

- Het voldoen aan de beheersvereisten van de organisatie. U kunt bijvoorbeeld een primaire site op een externe locatie installeren om de overdracht van implementatie-inhoud over een netwerk met een lage band breedte te beheren.  

     - Overweeg in plaats daarvan opties te gebruiken om de netwerk bandbreedte te beperken bij de overdracht van gegevens naar een distributie punt. De functionaliteit van inhouds beheer kan de nood zaak vervangen om extra sites te installeren.  


De volgende informatie kan u helpen bepalen wanneer u een primaire site installeert:  

- Een primaire site kan een zelfstandige primaire site of een onderliggende primaire site in een grotere hiërarchie zijn. Wanneer een primaire site lid is van een hiërarchie met een centrale beheersite, gebruiken de sites databasereplicatie om gegevens tussen de sites te repliceren. Tenzij u meer clients en apparaten moet ondersteunen dan één primaire site ondersteunt, kunt u overwegen om een zelfstandige primaire site te installeren. Nadat u een zelfstandige primaire site hebt geïnstalleerd, vouwt u deze uit als dat nodig is om aan een nieuwe centrale beheer site te rapporteren om uw implementatie te verg Roten.  

- Een primaire site ondersteunt alleen een centrale beheer site als een bovenliggende site.  

- Een primaire site ondersteunt alleen secundaire sites als onderliggende sites en ondersteunt meerdere secundaire sites.  

- Primaire sites zijn verantwoordelijk voor de verwerking van alle client gegevens van hun toegewezen clients.  

- Primaire sites gebruiken database replicatie om rechtstreeks met hun centrale beheer site te communiceren. Dit gedrag wordt automatisch geconfigureerd wanneer een nieuwe site wordt geïnstalleerd.  



##  <a name="determine-when-to-use-a-secondary-site"></a><a name="BKMK_ChooseSecondary"></a>Bepalen wanneer een secundaire site moet worden gebruikt  

Gebruik secundaire sites voor het beheren van de overdracht van implementatie-inhoud en client gegevens over netwerken met een lage band breedte.  

U beheert een secundaire site van een centrale beheer site of de directe bovenliggende primaire site van de secundaire site. Secundaire sites zijn gekoppeld aan een primaire site. U kunt ze niet verplaatsen naar een andere bovenliggende site zonder ze te verwijderen en ze vervolgens opnieuw te installeren als een onderliggende site onder de nieuwe primaire site.

U kunt echter inhoud routeren tussen twee peer-secundaire sites om te helpen de op bestanden gebaseerde replicatie van implementatie-inhoud te beheren. Om client gegevens naar een primaire site over te brengen, gebruikt de secundaire site replicatie op basis van een bestand. Een secundaire site gebruikt ook databasereplicatie om met de bovenliggende primaire site ervan te communiceren.  

Overweeg de installatie van een secundaire site om een van de volgende redenen:  

- U hebt geen lokaal connectiviteits punt nodig voor een gebruiker met beheerders rechten.  

- U moet de overdracht van implementatie-inhoud naar sites lager in de hiërarchie beheren.  

- U moet client informatie beheren die naar sites wordt verzonden, hoger in de hiërarchie.  

Als u geen secundaire site wilt installeren en u clients op externe locaties hebt, moet u rekening houden met de volgende opties:  

- Gebruik peer-to-peer-technologieën zoals Windows BranchCache  

- Distributie punten inschakelen voor bandbreedte regeling en planning   

Gebruik deze opties voor inhouds beheer met of zonder secundaire sites. Ze helpen de omvang van uw Configuration Manager-infra structuur te verkleinen. Zie [bepalen wanneer u opties voor inhouds beheer wilt gebruiken](#BKMK_ChooseSecondaryorDP)voor meer informatie over opties voor het beheer van inhoud in Configuration Manager.  


De volgende informatie helpt u te bepalen wanneer u een secundaire site installeert:  

- Als er geen lokaal exemplaar van SQL Server beschikbaar is, installeren secundaire site servers automatisch SQL Server Express tijdens de installatie van de site.  

- De installatie van de secundaire site wordt gestart vanuit de Configuration Manager-console, in plaats van Setup rechtstreeks op een computer uit te voeren.  

- Secundaire sites gebruiken een subset van de informatie in de site database. Dit gedrag vermindert de hoeveelheid gegevens die SQL repliceert tussen de bovenliggende primaire site en de secundaire site.  

- Secundaire sites ondersteunen de route ring van op bestanden gebaseerde inhoud naar andere secundaire sites die een gemeen schappelijke bovenliggende primaire site hebben.  

- De site systeem rollen van het beheer punt en distributie punt worden door secundaire site-installaties automatisch op de secundaire site server geïnstalleerd.  



##  <a name="determine-when-to-use-content-management-options"></a><a name="BKMK_ChooseSecondaryorDP"></a>Bepalen wanneer u opties voor inhouds beheer wilt gebruiken  

Als u clients op externe netwerklocaties hebt, overweeg dan het gebruik van een of meerdere opties voor inhoudbeheer in plaats van een primaire of secundaire site. De nood zaak om een site te installeren, wordt vaak door de volgende opties verwijderd:  

- Delivery Optimization voor Windows 10  

- Peer-cache Configuration Manager  

- Windows BranchCache  

- Distributie punten voor bandbreedte regeling configureren  

- Hand matig inhoud kopiëren naar distributie punten (inhoud vooraf plaatsen)  


Als een van de volgende voor waarden van toepassing is, kunt u overwegen om een distributie punt te implementeren in plaats van een andere-site te installeren:  

- Uw netwerk bandbreedte is voldoende om client computers op de externe locatie te laten communiceren met een beheer punt op de primaire site. Clients communiceren met een beheer punt om client beleid te downloaden, inventaris te verzenden, rapportage status te verzenden en detectie-informatie te verzenden.  

- Background Intelligent Transfer Service (BITS) biedt onvoldoende bandbreedte regeling voor uw netwerk vereisten.  

Zie [basis concepten voor inhouds beheer](fundamental-concepts-for-content-management.md)voor meer informatie over opties voor het beheer van inhoud in Configuration Manager.  



##  <a name="beyond-hierarchy-topology"></a><a name="bkmk_beyond"></a>Meer dan hiërarchie topologie  

In combi natie met uw initiële hiërarchie topologie moet u ook rekening houden met de volgende vragen:  

- Welke site systeem rollen bieden services of mogelijkheden van verschillende sites in de hiërarchie?  

- Hoe beheert u configuraties en mogelijkheden voor de gehele hiërarchie in uw infra structuur?  


De volgende algemene overwegingen worden behandeld in afzonderlijke artikelen. Deze informatie is belang rijk om te beïnvloeden of te worden beïnvloed door uw hiërarchie-ontwerp:  

- Wanneer u [computers en apparaten wilt beheren](../../clients/manage/manage-clients.md), moet u nagaan of de apparaten on-premises, in de Cloud of apparaten zijn die eigendom zijn van de gebruiker (BYOD). Bedenk daarnaast hoe u apparaten beheert die ondersteuning bieden voor meerdere beheer opties. U kunt bijvoorbeeld Windows 10-apparaten beheren met Configuration Manager of integratie met Microsoft Intune. Zie [een oplossing voor Apparaatbeheer kiezen](../choose-a-device-management-solution.md)voor meer informatie.  

- Krijg inzicht in de manier waarop uw beschik bare netwerk infrastructuur de gegevens stroom tussen externe locaties kan beïnvloeden. Zie [uw netwerk omgeving voorbereiden](../network/configure-firewalls-ports-domains.md)voor meer informatie. Denk ook na over de geografische locatie van uw gebruikers en apparaten en of ze toegang hebben tot uw infra structuur via uw on-premises netwerk of Internet.  

- Plan een inhouds infrastructuur om de inhoud die u implementeert, efficiënt te distribueren naar apparaten die u beheert. Deze inhoud kan toepassingen, software-updates of besturings systemen zijn. Zie [inhoud en infra structuur voor inhoud beheren](../../servers/deploy/configure/manage-content-and-content-infrastructure.md)voor meer informatie.  

- Bepaal welke [functies en mogelijkheden van Configuration Manager](../changes/features-and-capabilities.md) u wilt gebruiken. Voor verschillende functies zijn verschillende site systeem rollen of Windows-infra structuur vereist. Bepaal in een hiërarchie met meerdere sites waar u deze implementeert voor het meest efficiënte gebruik van uw netwerk-en Server bronnen.  

- Houd rekening met de beveiliging van gegevens en apparaten, met inbegrip van het gebruik van een open bare-sleutel infrastructuur (PKI). Zie [PKI-certificaat vereisten](../network/pki-certificate-requirements.md)voor meer informatie.  


Raadpleeg de volgende artikelen voor sitespecifieke configuraties:  

- [Plannen voor de SMS-provider](plan-for-the-sms-provider.md)  

- [De sitedatabase plannen](plan-for-the-site-database.md)  

- [Plan maken voor sitesysteemservers en sitesysteemrollen](plan-for-site-system-servers-and-site-system-roles.md)  

- [De beveiliging plannen](../security/plan-for-security.md)  

- [Netwerkbandbreedte beheren](manage-network-bandwidth.md) wanneer u inhoud implementeer binnen een site  


Denk na over configuraties die sites en hiërarchieën omvatten  

- [Opties voor hoge Beschik baarheid](../../servers/deploy/configure/high-availability-options.md) voor sites en hiërarchieën

- [Het Active Directory schema uitbreiden](../network/extend-the-active-directory-schema.md) en sites configureren voor het [publiceren van site gegevens](../../servers/deploy/configure/publish-site-data.md)  

- [Gegevensoverdracht tussen sites](data-transfers-between-sites.md)  

- [Basisprincipes voor beheer op basis van rollen](../../understand/fundamentals-of-role-based-administration.md)  

- [Clients op internet beheren](../../clients/manage/manage-clients-internet.md)  

