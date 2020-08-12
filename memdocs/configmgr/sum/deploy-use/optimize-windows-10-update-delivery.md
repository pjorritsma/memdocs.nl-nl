---
title: Levering van Windows 10-update optimaliseren
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van Configuration Manager voor het beheren van update-inhoud om actueel te blijven met Windows 10.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: b670cfaf-96a4-4fcb-9caa-0f2e8c2c6198
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6c42015880cae09be48feff9c42b6b2a0d2c8544
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129311"
---
# <a name="optimize-windows-10-update-delivery-with-configuration-manager"></a>De levering van Windows 10-updates optimaliseren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voor veel klanten is een succesvol pad voor het verkrijgen en blijven gebruiken van de maandelijkse updates voor Windows 10 gestart met een goede strategie voor het distribueren van inhoud met behulp van Configuration Manager. De omvang van de maandelijkse kwaliteits updates kan een probleem zijn bij grote organisaties. Er zijn een aantal technologieën beschikbaar die zijn bedoeld om de band breedte en netwerk belasting te verlagen om update levering te optimaliseren. In dit artikel worden deze technologieën beschreven, vergeleken en worden aanbevelingen gegeven om u te helpen bij het nemen van beslissingen die u kunt gebruiken.  
 
Windows 10 biedt verschillende soorten updates. Zie voor meer informatie [typen bijwerken in Windows Update voor bedrijven](/windows/deployment/update/waas-manage-updates-wufb#types-of-updates-managed-by-windows-update-for-business). Dit artikel richt zich op de Windows 10- *kwaliteits* updates met Configuration Manager. 


## <a name="express-update-delivery"></a>Levering van snelle updates

Down loads voor de kwaliteit van Windows 10-updates kunnen groot zijn. Elk pakket bevat alle eerder uitgebrachte oplossingen om consistentie en eenvoud te garanderen. Micro soft heeft de omvang van de inhoud van Windows 10 update verminderd die elke client downloadt met een functie met de naam Express. Express wordt vandaag gebruikt door miljoenen apparaten die rechtstreeks updates van de Windows Update-service halen en de download grootte aanzienlijk reduceren. Dit voor deel is ook beschikbaar voor klanten waarvan de clients niet rechtstreeks van de Windows Update-service worden gedownload. 

Configuration Manager heeft ondersteuning toegevoegd voor [bestanden voor snelle installatie](manage-express-installation-files-for-windows-10-updates.md) van Windows 10-kwaliteits updates in versie 1702. Voor de beste ervaring is het echter raadzaam Configuration Manager versie 1802 of hoger te gebruiken. Voor de beste prestaties van de download snelheid wordt u ook aangeraden Windows 10 versie 1703 of hoger te gebruiken. 

> [!NOTE]  
> De inhoud van de snelle versie is aanzienlijk groter dan de versie van het volledige bestand. Een bestand voor snelle installatie bevat alle mogelijke variaties voor elk bestand dat kan worden bijgewerkt. Als gevolg hiervan wordt de vereiste hoeveelheid schijf ruimte verhoogd voor updates in de bron van het update pakket en op distributie punten wanneer u snelle ondersteuning inschakelt in Configuration Manager. Hoewel de benodigde schijf ruimte op de distributie punten toeneemt, neemt de omvang van de inhoud die clients downloaden van deze distributie punten af. Clients downloaden alleen de bits die ze nodig hebben (deltas), maar niet de hele update.


## <a name="peer-to-peer-content-distribution"></a>Peer-to-peer-distributie van inhoud

Hoewel clients alleen de onderdelen downloaden die ze nodig hebben, kunt u Windows-updates in uw omgeving versnellen door gebruik te maken van peer-to-peer-distributie van inhoud. Het gebruik van peers als een download bron voor kwaliteits updates kan nuttig zijn voor omgevingen waar lokale distributie punten niet aanwezig zijn in externe kant oren. Dit gedrag voor komt dat alle clients inhoud downloaden vanaf een extern distributie punt via een trage WAN-verbinding. Het gebruik van peers kan ook nuttig zijn wanneer clients terugvallen op de Windows Update-service. Er is slechts één peer nodig om update-inhoud uit de cloud te downloaden voordat u deze beschikbaar maakt voor andere apparaten.

Configuration Manager ondersteunt veel peer-to-peer-technologieën, waaronder de volgende:
- Windows Delivery Optimization
- Peer-cache Configuration Manager
- Windows BranchCache  

In de volgende secties vindt u meer informatie over deze technologieën.

### <a name="windows-delivery-optimization"></a>Windows Delivery Optimization

[Optimalisatie van levering](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) is de belangrijkste Download technologie en peer-to-peer-distributie methode ingebouwd in Windows 10. Windows 10-clients kunnen inhoud ophalen van andere apparaten op het lokale netwerk waarmee dezelfde updates worden gedownload. U kunt met behulp [van de Windows-opties die beschikbaar zijn voor Delivery Optimization](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#delivery-optimization-options)clients configureren in groepen. Met deze groepering kan uw organisatie apparaten identificeren die mogelijk de beste kandidaten zijn om te voldoen aan peer-to-peer-aanvragen. Delivery Optimization vermindert de totale band breedte die wordt gebruikt om apparaten up-to-date te houden terwijl de download tijd wordt versneld.

> [!NOTE]  
> Delivery Optimization is een door de Cloud beheerde oplossing. Internet toegang tot de Cloud service voor leverings optimalisatie is een vereiste voor het gebruik van de peer-to-peer-functionaliteit. Zie [Veelgestelde vragen over Delivery Optimization](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)voor meer informatie over de benodigde Internet-eind punten. 

Voor de beste resultaten moet u de [Download modus](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#download-mode) voor de leverings optimalisatie mogelijk instellen op **groep (2)** en *groeps-id's*definiëren. In groeps modus kan peering meerdere interne subnetten tussen apparaten die deel uitmaken van dezelfde groep, inclusief apparaten in externe kant oren. Gebruik de [optie groeps-id](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#select-the-source-of-group-ids) voor het maken van uw eigen aangepaste groep, onafhankelijk van domeinen en AD DS sites. De groeps Download modus is de aanbevolen optie voor de meeste organisaties die de beste bandbreedte optimalisatie met leverings optimalisatie kunnen halen.

Het hand matig configureren van deze groeps-Id's is lastig wanneer clients via verschillende netwerken roamen. Configuration Manager versie 1802 heeft een nieuwe functie toegevoegd om het beheer van dit proces te vereenvoudigen door [grens groepen te integreren met leverings optimalisatie](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization). Wanneer een client actief is, wordt er naar het beheer punt gecommuniceerd om het beleid op te halen en worden de netwerk-en grens groeps gegevens verstrekt. Configuration Manager maakt een unieke ID voor elke grens groep. De site gebruikt de locatie gegevens van de client om de client-ID van de leverings optimalisatie automatisch te configureren met de grens-ID van de Configuration Manager. Wanneer de client naar een andere grens groep verdeelt, wordt deze omleiding naar het beheer punt en wordt deze automatisch opnieuw geconfigureerd met een nieuwe grens groep-ID. Met deze integratie kan bezorgings optimalisatie gebruikmaken van de gegevens van de Configuration Manager grens groep om een peer te vinden van waaruit updates moeten worden gedownload.

### <a name="delivery-optimization-starting-in-version-1910"></a><a name="bkmk_DO-1910"></a>Bezorgings optimalisatie vanaf versie 1910
<!--4699118-->
Vanaf Configuration Manager versie 1910 kunt u bezorgings optimalisatie gebruiken voor de distributie van alle Windows Update-inhoud voor clients met Windows 10 versie 1709 of hoger, niet alleen bestanden voor snelle installatie.

Als u Delivery Optimization voor alle installatie bestanden van Windows Update wilt gebruiken, schakelt u de volgende [client instellingen voor software-updates](../../core/clients/deploy/about-client-settings.md#software-updates)in:

- **Clients toestaan om Delta-inhoud te downloaden wanneer deze beschikbaar is** ingesteld op **Ja**.
- **Poort die clients gebruiken voor het ontvangen van aanvragen voor Delta-inhoud** die is ingesteld op 8005 (standaard) of een aangepast poort nummer.

> [!IMPORTANT]
> - Optimalisatie van levering moet zijn ingeschakeld (standaard) en niet worden overgeslagen. Zie [Windows Delivery Optimization Reference](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference)(Engelstalig) voor meer informatie.
> - Controleer uw [client instellingen voor Delivery Optimization](../../core/clients/deploy/about-client-settings.md#delivery-optimization) bij het wijzigen van de [client instellingen voor software-updates](../../core/clients/deploy/about-client-settings.md#software-updates) voor Delta-inhoud.
> - Delivery Optimization kan niet worden gebruikt voor Microsoft 365-apps client updates als Office COM is ingeschakeld. Office COM wordt door Configuration Manager gebruikt voor het beheren van updates voor Microsoft 365 apps-clients. U kunt de registratie van Office COM opheffen om het gebruik van leverings optimalisatie voor updates van Microsoft 365-apps toe te staan. Als Office COM is uitgeschakeld, worden software-updates voor Microsoft 365-apps beheerd door de standaard Office Automatische updates 2,0-geplande taak. Dit betekent dat Configuration Manager het installatie proces voor het bijwerken van Microsoft 365 apps niet onderdicteert of bewaakt. Configuration Manager blijven gegevens verzamelen van hardware-inventaris om het Office 365-dash board voor client beheer te vullen in de-console. Zie [office 365-clients inschakelen voor het ontvangen van updates van het Office CDN in plaats van Configuration Manager](https://docs.microsoft.com/deployoffice/manage-office-365-proplus-updates-with-configuration-manager#enable-office-365-clients-to-receive-updates-from-the-office-cdn-instead-of-configuration-manager)voor meer informatie over het deregistreren van Office com.
> - Wanneer u een CMG gebruikt voor de opslag van inhoud, worden de inhoud voor updates van derden niet gedownload naar clients als de instelling **Delta-inhoud downloaden wanneer de beschik bare** [client](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) is ingeschakeld. <!--6598587-->


### <a name="configuration-manager-peer-cache"></a>Peer-cache Configuration Manager

[Peer-cache](../../core/plan-design/hierarchy/client-peer-cache.md) is een functie van Configuration Manager waarmee clients rechtstreeks vanuit hun lokale Configuration Manager cache kunnen delen met andere clients inhoud. Peer-cache vervangt niet het gebruik van andere peer-caching-oplossingen zoals Windows BranchCache. Het werkt samen met hen om meer opties te bieden voor het uitbreiden van traditionele oplossingen voor inhouds implementatie, zoals distributie punten. Peer-cache vertrouwt niet op BranchCache. Als u BranchCache niet inschakelt of gebruikt, werkt peer-cache nog steeds.

> [!NOTE]  
> Clients kunnen alleen inhoud downloaden van peer-cache-clients die zich in hun huidige grens groep bevinden.  


### <a name="windows-branchcache"></a>Windows BranchCache
[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) is een technologie voor bandbreedte optimalisatie in Windows. Elke client heeft een cache en fungeert als een alternatieve bron voor inhoud. Apparaten op hetzelfde netwerk kunnen deze inhoud aanvragen. [Configuration Manager kunt BranchCache gebruiken](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache) om peers toe te staan van de bron inhoud van elkaar versus altijd contact opnemen met een distributie punt. Met BranchCache worden bestanden opgeslagen in de cache op elke afzonderlijke client en kunnen andere clients deze indien nodig ophalen. Met deze methode wordt de cache gedistribueerd in plaats van één punt om op te halen. Dit gedrag bespaart een aanzienlijke hoeveelheid band breedte en vermindert de tijd voor clients om de aangevraagde inhoud te ontvangen.



## <a name="selecting-the-right-peer-caching-technology"></a>De juiste peer-caching-technologie selecteren

Het selecteren van de juiste peer cache technologie voor bestanden voor snelle installatie is afhankelijk van uw omgeving en vereisten. Hoewel Configuration Manager alle bovenstaande peer-to-peer-technologieën ondersteunt, moet u deze gebruiken die het meest geschikt zijn voor uw omgeving. Voor de meeste klanten, ervan uitgaande dat clients kunnen voldoen aan de Internet vereisten voor de optimalisatie van de levering, moet de ingebouwde peer-caching van Windows 10 met leverings optimalisatie voldoende zijn. Als uw clients niet aan deze Internet vereisten voldoen, kunt u overwegen de Configuration Manager-functie voor peer-cache te gebruiken. Als u momenteel gebruikmaakt van BranchCache met Configuration Manager en deze voldoet aan uw behoeften, kunnen Express-bestanden met BranchCache de juiste optie zijn. 

### <a name="peer-cache-comparison-chart"></a>Vergelijking diagram peer-cache


| Functionaliteit  | Delivery optimization  | Peer-cache  | BranchCache  |
|---------|---------|---------|---------|
| Ondersteund in meerdere subnetten | Ja | Ja | Nee |
| Bandbreedte regeling | Ja (systeem eigen) | Ja (via BITS) | Ja (via BITS) |
| Ondersteuning voor gedeeltelijke inhoud | Ja, voor alle ondersteunde inhouds typen die in de volgende rij van deze kolom worden weer gegeven. | Alleen voor Microsoft 365-apps en snelle updates | Ja, voor alle ondersteunde inhouds typen die in de volgende rij van deze kolom worden weer gegeven. |
| Ondersteunde inhouds typen | **Via ConfigMgr:** </br> -Snelle updates </br> -Alle Windows-updates (vanaf versie 1910). Dit omvat geen updates van Microsoft 365-apps.</br> </br> **Via micro soft Cloud:**</br> -Windows-en beveiligings updates</br> -Stuur Programma's</br> -Windows Store-apps</br> -Windows Store voor bedrijven-apps | Alle inhouds typen van ConfigMgr, inclusief afbeeldingen die zijn gedownload in [Windows PE](../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md) | Alle inhouds typen van ConfigMgr, behalve afbeeldingen |
| Cache grootte op schijf beheer | Ja | Ja | Ja |
| Detectie van een peer bron | Automatisch | Hand matig (instelling client agent) | Automatisch |
| Peer-detectie | Via Delivery Optimization Cloud service (Internet toegang vereist) | Via beheer punt (gebaseerd op client grens groepen) | Cast |
| Rapporten | Ja (met Desktop Analytics) | Dash board client gegevens bronnen ConfigMgr | Dash board client gegevens bronnen ConfigMgr |
| Besturings element voor WAN-gebruik | Ja (systeem eigen, kan worden beheerd via groeps beleids instellingen) | Grensgroepen | Alleen subnet-ondersteuning |
| Beheer via ConfigMgr | Gedeeltelijk (instelling client agent) | Ja (instelling client agent) | Ja (instelling client agent) |



## <a name="conclusion"></a>Conclusie

Micro soft raadt u aan om de levering van de kwaliteits updates voor Windows 10 te optimaliseren met Configuration Manager snelle installatie bestanden en een peer-caching-technologie, indien nodig. Deze aanpak moet de uitdagingen van Windows 10-apparaten voor het downloaden van grote inhoud voor het installeren van kwaliteits updates afwijzen. Het is ook raadzaam om Windows 10-apparaten up-to-date te houden door kwaliteits updates te implementeren. Met deze procedure wordt de Delta van de kwaliteits update-inhoud die elke maand nodig is voor apparaten, gereduceerd. Het verminderen van deze inhouds Delta veroorzaakt een kleinere Download grootte van distributie punten of peer bronnen. 

Vanwege de aard van de bestanden voor snelle installatie is de inhouds grootte aanzienlijk groter dan traditionele, zelfstandige bestanden. Met deze grootte worden de download tijden voor een langere update van de Windows Update-service naar de Configuration Manager-site server. De hoeveelheid schijf ruimte die nodig is voor zowel de site server als de distributie punten neemt ook toe. De totale tijd die nodig is voor het downloaden en distribueren van kwaliteits updates is langer. De voor delen van het apparaat moeten echter merkbaar zijn tijdens het downloaden en installeren van kwaliteits updates van Windows 10-apparaten. Zie [bestanden voor snelle installatie gebruiken](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc708456(v=ws.10)?#using-express-installation-files)voor meer informatie.

Als de server zijde van grotere updates blok keren is voor de acceptatie van snelle ondersteuning, maar de voor delen van het apparaat zijn essentieel voor uw bedrijf en omgeving, raadt micro soft u aan om Windows Update te gebruiken [voor bedrijven](integrate-windows-update-for-business-windows-10.md) met Configuration Manager. Windows Update voor bedrijven biedt alle voor delen van Express zonder de nood zaak om bestanden voor snelle installatie te downloaden, op te slaan en te distribueren in uw omgeving. Clients downloaden inhoud rechtstreeks vanuit de Windows Update-service, waardoor de optimalisatie van de levering nog steeds kan worden gebruikt.



## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a>Veelgestelde vragen

#### <a name="how-do-windows-express-downloads-work-with-configuration-manager"></a>Hoe werkt Windows Express-down loads met Configuration Manager?

De Windows Update Agent (WUA) vraagt eerst snelle inhoud op. Als de snelle update niet kan worden geïnstalleerd, kan deze terugvallen op de volledige update.  

1. De Configuration Manager-client vertelt WUA het downloaden van de update-inhoud. Wanneer WUA een snelle down load initieert, downloadt het eerst een stub (bijvoorbeeld `Windows10.0-KB1234567-<platform>-express.cab` ), die deel uitmaakt van het Express-pakket.  

2. WUA geeft deze stub door aan het installatie programma van Windows Update, CBS (Component-Based Servicing). CBS gebruikt de stub om een lokale inventarisatie uit te voeren, waarbij de Deltas van het bestand op het apparaat worden vergeleken met wat er nodig is om naar de meest recente versie van het bestand te gaan dat wordt aangeboden.  

3. CBS vraagt vervolgens WUA om de vereiste bereiken van een of meer Express. psf-bestanden te downloaden.  

4. Als Delivery Optimization is ingeschakeld en peers detecteert de benodigde bereiken, wordt de client vanaf peers onafhankelijk van de Configuration Manager-client gedownload. Als Delivery Optimization is uitgeschakeld of als er geen peers zijn die de benodigde bereiken hebben, worden deze bereiken door de ConfigMgr-client gedownload van een lokaal distributie punt (of een peer-of Microsoft Update). De bereiken worden door gegeven aan de Windows Update-Agent, waardoor deze kunnen worden toegepast op CBS om de bereiken toe te passen.


#### <a name="why-are-the-express-files-psf-so-large-when-stored-on-configuration-manager-peer-sources-in-the-ccmcache-folder"></a>Waarom worden de Express-bestanden (. psf) zo groot als ze worden opgeslagen op Configuration Manager peer bronnen in de map ccmcache?

De Express-bestanden (. psf) zijn verspreide bestanden. Controleer de eigenschap **grootte op schijf** van het bestand om na te gaan welke ruimte op de schijf door het bestand wordt gebruikt. De eigenschap grootte op schijf moet aanzienlijk kleiner zijn dan de grootte waarde.  


#### <a name="does-configuration-manager-support-express-installation-files-with-windows-10-feature-updates"></a>Ondersteunt Configuration Manager snelle installatie bestanden met updates voor Windows 10-onderdelen?

Nee, Configuration Manager momenteel alleen bestanden voor snelle installatie met kwaliteits updates voor Windows 10 ondersteunt.  


#### <a name="how-much-disk-space-is-needed-per-quality-update-on-the-site-server-and-distribution-points"></a>Hoeveel schijf ruimte is er nodig per kwaliteits update op de site server en distributie punten?

Dat hangt ervan af. Voor elke kwaliteits update worden zowel de volledige als de snelle versie van de update opgeslagen op servers. Windows 10-kwaliteits updates zijn cumulatief, waardoor de grootte van deze bestanden elke maand toeneemt. Plan voor mini maal 5 GB per update per taal. 


#### <a name="do-configuration-manager-clients-still-benefit-from-express-installation-files-when-falling-back-to-the-windows-update-service"></a>Profiteren Configuration Manager-clients nog steeds van de bestanden voor snelle installatie wanneer u terugkeert naar de Windows Update-service?

Ja. Als u de volgende implementatie optie voor software-updates gebruikt, blijven clients nog steeds gebruikmaken van snelle updates en Delivery Optimization wanneer ze terugvallen op de Cloud service:  

**Als er geen software-updates beschikbaar zijn op het distributie punt in de huidige, neighbor-of site groepen, downloadt u inhoud van micro soft updates**


#### <a name="why-is-express-file-content-not-downloaded-for-existing-updates-after-i-enable-express-file-support"></a>Waarom wordt de inhoud van Express-bestanden niet gedownload voor bestaande updates nadat ik ondersteuning voor Express-bestanden heb ingeschakeld? 

De wijzigingen worden pas van kracht wanneer nieuwe updates worden gesynchroniseerd en geïmplementeerd na het inschakelen van de ondersteuning.


#### <a name="is-there-any-way-to-see-how-much-content-is-downloaded-from-peers-using-delivery-optimization"></a>Is er een manier om te zien hoeveel inhoud er wordt gedownload van peers met behulp van leverings optimalisatie?
Windows 10, versie 1703 (en hoger) bevat twee nieuwe Power shell-cmdlets: **Get-DeliveryOptimizationPerfSnap** en **Get-DeliveryOptimizationStatus**. Deze cmdlets bieden meer inzicht in de bezorgings optimalisatie en het cache gebruik. Zie [Delivery Optimization voor Windows 10 updates](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#the-cloud-service-doesnt-see-other-peers-on-the-network) voor meer informatie.


#### <a name="how-do-clients-communicate-with-delivery-optimization-over-the-network"></a>Hoe kunnen clients communiceren met Delivery Optimization via het netwerk?
Zie [Veelgestelde vragen over Delivery Optimization](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)voor meer informatie over de netwerk poorten, proxy vereisten en hostnamen voor firewalls.

## <a name="log-files"></a>Logboekbestanden

Gebruik de volgende logboek bestanden om Delta downloads te bewaken:

- WUAHandler.log
- DeltaDownload. log

## <a name="next-steps"></a>Volgende stappen

- [Software-updates implementeren](deploy-software-updates.md)
- [Software-updates automatisch implementeren](automatically-deploy-software-updates.md)
