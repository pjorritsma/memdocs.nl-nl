---
title: Clients toewijzen aan een site
titleSuffix: Configuration Manager
description: Clients toewijzen aan een site in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: ba9b623f-6e86-4006-93f2-83d563de0cd0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ab2270435ac13585cb0b7d3271f1faa02cc728d3
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075741"
---
# <a name="how-to-assign-clients-to-a-site-in-configuration-manager"></a>Clients toewijzen aan een site in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Nadat een Configuration Manager-client is geïnstalleerd, moet deze worden toegevoegd aan een Configuration Manager primaire site voordat u deze kunt beheren. De site waaraan een client wordt toegevoegd, wordt de *toegewezen site*genoemd. Clients kunnen niet worden toegewezen aan een centrale beheersite of aan een secundaire site.  

Het toewijzings proces vindt plaats nadat de client is geïnstalleerd en bepaalt welke site de client computer beheert. U kunt de client ofwel rechtstreeks toewijzen aan een site, of u kunt automatische site toewijzing gebruiken waarbij de client automatisch een geschikte site vindt op basis van de huidige netwerk locatie of een terugval site die voor de hiërarchie is geconfigureerd.

Wanneer u de client voor mobiele apparaten installeert tijdens Configuration Manager registratie, wordt het apparaat altijd automatisch toegewezen aan een site. Wanneer u de-client op een computer installeert, kunt u kiezen of u de-client aan een-site wilt toewijzen. De client blijft niet-beheerd totdat de sitetoewijzing is voltooid als de client is geïnstalleerd, maar niet toegewezen.  
 

> [!NOTE]  
>  Wijs clients altijd toe aan sites met dezelfde versie van Configuration Manager. Vermijd het toewijzen van een Configuration Manager-client van een nieuwere versie aan een site vanuit een oudere versie.   Indien nodig werkt u de primaire site bij naar dezelfde Configuration Manager versie die u voor de clients gebruikt.  

Nadat de client aan een site is toegewezen, blijft deze toegewezen aan die site, zelfs als de client zijn IP-adres verandert en naar een andere site roamt. Alleen een beheerder kan de client hand matig toewijzen aan een andere site of de client toewijzing verwijderen.  

> [!WARNING]  
>  Een uitzondering op een client die blijft toegewezen aan een site, geldt voor als u de client op een Windows Embedded-apparaat toewijst als de schrijffilters zijn ingeschakeld. Als u schrijffilters niet eerst uitschakelt voordat u de client toewijst, keert de sitetoewijzingsstatus van de client terug naar de oorspronkelijke status wanneer het apparaat de volgende keer opnieuw wordt opgestart.  
>   
>  Als de client bijvoorbeeld geconfigureerd is voor automatische sitetoewijzing, wordt er tijdens het opstarten een nieuwe toewijzing uitgevoerd en is het mogelijk dat de client aan een andere site wordt toegewezen. Als de client niet is geconfigureerd voor automatische site toewijzing, maar hand matige site toewijzing vereist, moet u de client hand matig opnieuw toewijzen na het opstarten, zodat u deze client opnieuw kunt beheren door gebruik te maken van Configuration Manager.  
>   
>  U kunt dit gedrag vermijden door de schrijffilters uit te schakelen voordat u de client op ingesloten apparaten toewijst. Nadat u hebt geverifieerd dat de sitetoewijzing is geslaagd, schakelt u de schrijffilters opnieuw in.  

Als de client toewijzing mislukt, blijft de client software geïnstalleerd, maar wordt deze niet beheerd. Een client wordt als niet-beheerd beschouwd als deze geïnstalleerd is, maar niet is toegewezen aan een site, of als deze aan een site is toegewezen, maar niet kan communiceren met een beheerpunt.  

##  <a name="using-manual-site-assignment-for-computers"></a>Handmatige sitetoewijzing gebruiken voor computers  
 U kunt clientcomputers handmatig toewijzen aan een site aan de hand van de volgende twee methoden:  

-   Gebruik een clientinstallatie-eigenschap die de sitecode specificeert.  

-   Geef de sitecode op in het Configuratiescherm, in **Configuration Manager**.  

> [!NOTE]  
>  Als u een client computer hand matig toewijst aan een Configuration Manager site code die niet bestaat, mislukt de site toewijzing.   

##  <a name="using-automatic-site-assignment-for-computers"></a><a name="BKMK_AutomaticAssignment"></a>Automatische site toewijzing gebruiken voor computers  
 Automatische sitetoewijzing kan zich voordoen tijdens clientimplementatie of wanneer u klikt op **Site zoeken** in het tabblad **Geavanceerd** van de **Eigenschappen van Configuration Manager** in het Configuratiescherm. De Configuration Manager-client vergelijkt zijn eigen netwerk locatie met de grenzen die in de Configuration Manager-hiërarchie zijn geconfigureerd. Als de netwerklocatie van de client binnen een grensgroep valt die voor sitetoewijzing is ingeschakeld, of als de hiërarchie voor een terugvalsite is geconfigureerd, wordt de client automatisch toegewezen naar die site zonder dat u een sitecode moet opgeven.  

 U kunt grenzen configureren door een of meer van de volgende opties te gebruiken:  

-   IP-subnet  

-   Active Directory-site  

-   IPv6-voorvoegsel  

-   IP-adresbereik  

> [!NOTE]  
>  Als een Configuration Manager-client meerdere netwerk adapters heeft en daarom meerdere IP-adressen heeft, wordt het IP-adres dat wordt gebruikt voor het evalueren van de toewijzing van de client site wille keurig toegewezen.  

 Zie [site grenzen en grens groepen voor Configuration Manager definiëren](../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)voor informatie over het configureren van grens groepen voor site toewijzing en het configureren van een terugval site voor automatische site toewijzing.  

 Configuration Manager-clients die automatische site toewijzing gebruiken, proberen site grens groepen te vinden die naar Active Directory Domain Services worden gepubliceerd. Als dit mislukt (bijvoorbeeld als het Active Directory schema niet is uitgebreid voor Configuration Manager of als de clients werkgroepcomputers zijn), kunnen clients informatie over de grens groep ophalen van een beheer punt.  

 U kunt een beheerpunt opgeven voor clientcomputers voor gebruik wanneer ze worden geïnstalleerd. Clients kunnen ook een beheerpunt zoeken door gebruik te maken van DNS-publishing of WINS.  

 Als de client geen site kan vinden die is gekoppeld met een grensgroep die de netwerklocatie ervan bevat en als de hiërarchie geen terugvalsite heeft, zal de client elke 10 minuten opnieuw zoeken totdat deze kan worden toegewezen aan een site.  

 Configuration Manager-client computers kunnen niet automatisch worden toegewezen aan een site als een van de volgende van toepassing is, en ze moeten vervolgens hand matig worden toegewezen:  

-   Ze zijn momenteel toegewezen aan een site.  

-   Ze zijn verbonden met het internet of geconfigureerd als clients met alleen internetverbinding.  

-   Hun netwerklocatie valt niet binnen één van de geconfigureerde grensgroepen in de Configuration Manager-hiërarchie en er is geen terugvalsite voor de hiërarchie.  

##  <a name="completing-site-assignment-by-checking-site-compatibility"></a>Sitetoewijzing voltooien door het controleren van de sitecompatibiliteit  
 Nadat een client zijn toegewezen site heeft gevonden, worden de versie en het besturings systeem van de client gecontroleerd om ervoor te zorgen dat een Configuration Manager-site deze kan beheren. Configuration Manager kan bijvoorbeeld Configuration Manager 2007-clients, System Center 2012 Configuration Manager clients of clients met Windows 2000 niet beheren.  

 Site toewijzing mislukt als u een client toewijst die Windows 2000 uitvoert op een Configuration Manager-site. Wanneer u een Configuration Manager 2007-client of een System Center 2012 Configuration Manager-client toewijst aan een Configuration Manager-site (current branch), kan de site toewijzing de automatische client upgrade ondersteunen. Voordat de oudere clients worden bijgewerkt naar een Configuration Manager-client (current branch), kan Configuration Manager deze client echter niet beheren door client instellingen, toepassingen of software-updates te gebruiken.  

> [!NOTE]  
>  U moet automatische client upgrade voor de hiërarchie configureren om de site toewijzing van een Configuration Manager 2007 of een System Center 2012 Configuration Manager-client aan een Configuration Manager-site (current branch) te ondersteunen. Zie [clients voor Windows-computers bijwerken voor](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)meer informatie.  

Configuration Manager controleert ook of u de Configuration Manager-client (current branch) hebt toegewezen aan een site die deze ondersteunt. De volgende scenario's kunnen zich voordoen tijdens de migratie van eerdere versies van Configuration Manager.  

- Scenario: u hebt automatische site toewijzing gebruikt en uw grenzen overlappen met de beperkingen die zijn gedefinieerd in een eerdere versie van Configuration Manager.  

   In dit geval probeert de client automatisch een Configuration Manager-site (current branch) te vinden.  

   De client controleert eerst Active Directory Domain Services en als er een Configuration Manager-site (current branch) wordt gevonden, is de site toewijzing geslaagd. Als dit mislukt (bijvoorbeeld als de Configuration Manager-site niet is gepubliceerd of als de computer een werkgroepcomputer is), controleert de client vervolgens of er site-informatie is van het toegewezen beheer punt.  

  > [!NOTE]  
  >  U kunt een beheer punt toewijzen aan de client tijdens de client installatie door gebruik te maken van de client. msi-eigenschap **SMSMP =&lt;server_name>**.  

   De sitetoewijzing mislukt als deze twee methoden mislukken. In dat geval moet u de client handmatig toewijzen.  

- Scenario: u hebt de Configuration Manager (current branch) toegewezen met een specifieke site code in plaats van automatische site toewijzing en u hebt per ongeluk een site code opgegeven voor een versie van Configuration Manager ouder dan System Center 2012 R2 Configuration Manager.  

   In dit geval mislukt de site toewijzing en moet u de client hand matig opnieuw toewijzen aan een Configuration Manager-site (current branch).  

  Voor de controle van de sitecompatibiliteit gelden de volgende voorwaarden:  

- De client heeft toegang tot site-informatie die naar Active Directory Domain Services is gepubliceerd.  

- De client kan communiceren met een beheerpunt in de site.  

  Als de controle van de site compatibiliteit niet kan worden voltooid, mislukt de site toewijzing en blijft de client niet-beheerd totdat de controle van de site compatibiliteit opnieuw wordt uitgevoerd en slaagt.  

  De uitzondering op het uitvoeren van de controle van de sitecompatibiliteit doet zich voor wanneer een client voor een beheerpunt op internet is geconfigureerd. In dit geval wordt er geen controle van de site compatibiliteit uitgevoerd. Als u clients toewijst aan een site die sitesystemen op internet bevat en u geeft een beheerpunt op internet op, zorg er dan voor dat u de client aan de juiste site toewijst. Als u de client per ongeluk toewijst aan een Configuration Manager 2007-site, een System Center 2012 Configuration Manager-site of een Configuration Manager-site die geen site systeem rollen op internet heeft, zal de client onbeheerd zijn.  

##  <a name="locating-management-points"></a>Zoeken naar beheerpunten  
 Nadat een client is toegewezen aan een site, zoekt deze een beheerpunt in de site.  

 Client computers downloaden een lijst van beheer punten waarmee ze verbinding kunnen maken in de site. Dit gebeurt wanneer de client opnieuw wordt opgestart, of om de 25 uur, of als de client een netwerk wijziging detecteert, bijvoorbeeld wanneer de computer de verbinding met het netwerk verbreekt en opnieuw verbinding maakt of een nieuw IP-adres ontvangt. De lijst omvat beheerpunten op het intranet en of ze clientverbindingen via HTTP of HTTPS accepteren. Wanneer de client computer zich op het Internet bevindt en de client nog geen lijst met beheer punten heeft, maakt deze verbinding met het opgegeven beheer punt op internet om een lijst met beheer punten te verkrijgen. Als de client een lijst beheerpunten heeft voor de toegewezen site, wordt er één geselecteerd om verbinding mee te maken:  

-   De client geeft de voorkeur aan HTTPS-beheerpunten boven HTTP-beheerpunten als de client is verbonden met het intranet en een geldig PKI-certificaat heeft dat het kan gebruiken. Vervolgens zoekt de client het dichtstbijzijnde beheerpunt op basis van het forest-lidmaatschap.  

-   Wanneer de client op internet is, kiest het wille keurig een van de beheer punten op internet.  

Clients voor mobiele apparaten die zijn Inge schreven door Configuration Manager, kunnen alleen verbinding maken met één beheer punt in hun toegewezen site en nooit verbinding maken met beheer punten op secundaire sites. Deze clients verbinden altijd via HTTPS en het beheerpunt moet worden geconfigureerd om clientverbindingen via het internet te accepteren. Wanneer er meer dan één beheer punt voor clients van mobiele apparaten in de primaire site is, kiest Configuration Manager wille keurig een van deze beheer punten tijdens de toewijzing. de client van het mobiele apparaat blijft hetzelfde beheer punt gebruiken.  

De client is een beheerde client als deze clientbeleid heeft gedownload van een beheerpunt in de site.  

##  <a name="downloading-site-settings"></a>Site-instellingen downloaden  
 Nadat de sitetoewijzing is voltooid en de client een beheerpunt heeft gevonden, downloadt een clientcomputer die Active Directory Domain Services voor de controle van de sitecompatibiliteit gebruikt, clientgerelateerde site-instellingen voor de toegewezen site. Deze instellingen omvatten de selectiecriteria van het clientcertificaat, of er een certificaatintrekkingslijst wordt gebruikt, en de door de client aangevraagde poortnummers. De client blijft deze instellingen periodiek controleren.  

 Als clientcomputers geen site-instellingen kunnen verkrijgen van Active Directory Domain Services, downloaden ze deze van hun beheerpunt. Client computers kunnen de site-instellingen ook verkrijgen wanneer ze worden geïnstalleerd met behulp van client push of u kunt ze hand matig opgeven met behulp van CCMSetup. exe en eigenschappen van client installatie. Zie [over eigenschappen van client installatie](../../../core/clients/deploy/about-client-installation-properties.md)voor meer informatie over de client installatie-eigenschappen.  

##  <a name="downloading-client-settings"></a>Clientinstellingen downloaden  
 Alle clients downloaden het standaard clientinstellingenbeleid en elk ander aangepast clientinstellingenbeleid dat van toepassing is. Software Center is afhankelijk van dit clientconfiguratiebeleid voor Windows-computers en gebruikers zullen een melding ontvangen dat Software Center niet kan worden uitgevoerd totdat deze configuratie-informatie is gedownload. Afhankelijk van de geconfigureerde clientinstellingen kan het initiële downloaden van de clientinstellingen enige tijd duren. Sommige clientbeheertaken kunnen mogelijk niet worden uitgevoerd totdat dit proces is voltooid.  

##  <a name="verifying-site-assignment"></a>Sitetoewijzing controleren  
 Met een van de volgende methoden kunt u een geslaagde site toewijzing controleren:  

-   Gebruik voor clients op Windows-computers Configuration Manager in het configuratie scherm en controleer of de site code juist wordt weer gegeven op het tabblad **site** .  

-   Voor client computers, in de werk ruimte **activa en naleving** > knoop punt **apparaten** , controleert u of op de computer **Ja** wordt weer gegeven voor de kolom **client** en de juiste code van de primaire site voor de kolom **site code** .  

-   Voor mobiele apparaatclients kunt u in de werkruimte **Activa en naleving** via de verzameling **Alle mobiele apparaten** controleren of voor het mobiele apparaat **Ja** in de kolom **Client** wordt weergegeven en of de juiste code van de primaire site wordt weergegeven in de kolom **Sitecode** .  

-   Gebruik de rapporten voor de clienttoewijzing en de inschrijving van mobiele apparaten.  

-   Voor clientcomputers gebruikt u het bestand LocationServices.log op de client.  

##  <a name="roaming-to-other-sites"></a>Roaming naar andere sites  
 Wanneer clientcomputers op het intranet aan een primaire site worden toegewezen maar binnen een grensgroep vallen die voor een andere site is geconfigureerd vanwege een gewijzigde netwerklocatie, hebben deze naar een andere site gezworven. Wanneer deze site een secundaire site is van de hun toegewezen site, kunnen clients met behulp van een beheerpunt in de secundaire site clientbeleid downloaden en clientgegevens uploaden, waardoor wordt voorkomen dat deze gegevens via een mogelijk traag netwerk worden verzonden. Als deze clients echter tot binnen de grenzen zwerven van een andere primaire site of een secundaire site die geen onderliggende site is van de aan hen toegewezen site, gebruiken deze clients altijd een beheerpunt in de aan hen toegewezen site om clientbeleid te downloaden en gegevens naar hun site te uploaden.  

 Deze naar andere sites (alle primaire en secundaire sites) zwervende clientcomputers kunnen altijd gebruik maken van beheerpunten in andere sites voor verzoeken om de locatie van inhoud. Beheerpunten in de actuele site kunnen clients een lijst met distributiepunten geven die over de inhoud beschikken waarom clients verzoeken.  

 Voor client computers die zijn geconfigureerd voor client beheer op internet en voor mobiele apparaten en Mac-computers die zijn Inge schreven door Configuration Manager, kunnen deze clients alleen communiceren met beheer punten in hun toegewezen site. Deze clients communiceren nooit met beheerpunten in secundaire sites of andere primaire sites.  
