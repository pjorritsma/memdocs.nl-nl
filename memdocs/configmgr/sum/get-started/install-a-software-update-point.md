---
title: Een software-update punt installeren en configureren
titleSuffix: Configuration Manager
description: Voor primaire sites is een software-update punt op de centrale beheer site vereist voor de evaluatie van de naleving van software-updates en voor het implementeren van software-updates op clients.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b099a645-6434-498f-a408-1d438e394396
ms.openlocfilehash: 0cddb8df51624a562597da17ea310db0a26081f3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715471"
---
# <a name="install-and-configure-a-software-update-point"></a>Een software-update punt installeren en configureren  

*Van toepassing op: Configuration Manager (huidige vertakking)*


> [!IMPORTANT]  
>  Voordat u de site systeemrol van het software-update punt (SUP) installeert, moet u controleren of de server voldoet aan de vereiste afhankelijkheden en de infra structuur van het software-update punt op de site bepaalt. Zie [software-updates plannen](../plan-design/plan-for-software-updates.md)voor meer informatie over het plannen van software-updates en het bepalen van uw software-update punt infrastructuur.  

 Het software-update punt is vereist op de centrale beheer site en op de primaire sites om de nalevings beoordeling van software-updates in te scha kelen en om software-updates te implementeren op clients. Het software-updatepunt is optioneel op secundaire sites. De sitesysteemrol van het software-updatepunt moet op een server worden gemaakt waar WSUS op is geïnstalleerd. Het software-updatepunt communiceert met de WSUS-services om de software-update-instellingen te configureren en om de synchronisatie van de metagegevens van software-updates aan te vragen. Wanneer u een Configuration Manager-hiërarchie hebt, installeert en configureert u het software-update punt eerst op de centrale beheer site en vervolgens op onderliggende primaire sites, en vervolgens optioneel op secundaire sites. Als u een zelfstandige primaire site hebt, en geen centrale beheersite, dient u eerst het software-updatepunt op de primaire site, en vervolgens optioneel op secundaire sites, te installeren en configureren. Sommige instellingen zijn alleen beschikbaar wanneer u het software-updatepunt op een site op het hoogste niveau configureert. Er zijn verschillende opties die u moet overwegen, afhankelijk van waar u het software-updatepunt hebt geïnstalleerd.  

> [!IMPORTANT]  
>  U kunt meerdere software-updatepunten op een site installeren. Het eerste software-updatepunt dat u installeert, wordt geconfigureerd als de synchronisatiebron: dit software-updatepunt synchroniseert de updates van Microsoft Update of van de upstream-synchronisatiebron. De andere software-updatepunten op de site zijn geconfigureerd als replica's van het eerste software-updatepunt. Daarom zijn sommige instellingen niet beschikbaar na het installeren en configureren van het oorspronkelijke software-updatepunt.  

> [!IMPORTANT]  
>  Het is niet mogelijk om de site systeemrol van het software-update punt te installeren op een server die is geconfigureerd en gebruikt als zelfstandige WSUS-server of met behulp van een software-update punt om WSUS-clients rechtstreeks te beheren. Bestaande WSUS-servers worden alleen ondersteund als upstream-synchronisatie bronnen voor het actieve software-update punt. Zie [synchroniseren vanaf een gegevens bron locatie stroomopwaarts](#BKMK_wsussync)

 U kunt de sitesysteemrol van het software-updatepunt toevoegen aan een bestaande sitesysteemserver of u kunt een nieuwe sitesysteemrol maken. Selecteer **Software-update punt**op de pagina **selectie van systeem rollen** van de **wizard site systeem server maken** of de **wizard site systeem rollen toevoegen**, afhankelijk van of u de site systeemrol toevoegt aan een nieuwe of bestaande site server. vervolgens configureert u de instellingen van het software-update punt in de wizard. De instellingen verschillen, afhankelijk van de versie van Configuration Manager die u gebruikt. Zie [site systeem rollen installeren](../../core/servers/deploy/configure/install-site-system-roles.md)voor meer informatie over het installeren van site systeem rollen.  

 Gebruik de volgende secties voor informatie over de software-updatepuntinstellingen op een site.  

## <a name="proxy-server-settings"></a>Proxyserverinstellingen  
 U kunt de proxyserver instellingen configureren op verschillende pagina's van de **wizard site systeem server maken** of de **wizard site systeem rollen toevoegen** , afhankelijk van de versie van Configuration Manager die u gebruikt.  

-   U moet de proxyserver configureren en vervolgens opgeven wanneer de proxyserver moet worden gebruikt voor software-updates. Configureer de volgende instellingen:  

    -   Configureer de proxyserverinstellingen op de pagina **Proxy** van de wizard of op het tabblad **Proxy** in de sitesysteemeigenschappen. De proxyserver instellingen zijn specifiek voor een site systeem, wat betekent dat alle site systeem rollen de proxyserver instellingen gebruiken die u opgeeft.  

    -   Geef op of de proxy server moet worden gebruikt wanneer Configuration Manager de software-updates synchroniseert en wanneer het inhoud downloadt door gebruik te maken van een regel voor automatische implementatie. Configureer de proxyserverinstellingen van het software-updatepunt op de pagina **Proxy- en accountinstellingen** van de wizard of op het tabblad **Proxy- en accountinstellingen** in de eigenschappen van het software-updatepunt.  

        > [!NOTE]  
        >  De instelling **Een proxyserver gebruiken wanneer inhoud wordt gedownload via automatische implementatieregels** is beschikbaar, maar wordt niet gebruikt voor een software-updatepunt op een secundaire site. Alleen het software-updatepunt op de centrale beheersite en de primaire site downloadt inhoud van de Microsoft Update-pagina.  

> [!IMPORTANT]  
>  Standaard wordt het account **Lokaal systeem** voor de server waarop een automatische implementatieregel is gemaakt, gebruikt om verbinding te maken met het internet en software-updates te downloaden wanneer de automatische implementatieregels worden uitgevoerd. Als dit account geen toegang tot internet heeft, kunnen de software-updates niet worden gedownload en wordt de volgende vermelding in het logboekbestand ruleengine.log opgeslagen: **Kan de update niet downloaden van internet. Fout = 12007**. Configureer de referenties om verbinding te maken met de proxyserver wanneer het lokale systeemaccount geen internettoegang heeft.  


## <a name="wsus-settings"></a>WSUS-instellingen  
 U moet de WSUS-instellingen configureren op verschillende pagina's van de **wizard site systeem server maken** of de **wizard site systeem rollen toevoegen** , afhankelijk van de versie van Configuration Manager die u gebruikt, en in sommige gevallen, alleen in de eigenschappen voor het software-update punt, ook wel de eigenschappen van software-update punt componenten genoemd. Gebruik de informatie in de volgende secties om de WSUS-instellingen te configureren.  

### <a name="wsus-port-settings"></a><a name="BKMK_wsusport"></a>WSUS-poortinstellingen  
 U moet de WSUS-poortinstellingen configureren op de pagina Software-updatepunt van de wizard of in de eigenschappen van het software-updatepunt. Gebruik de volgende procedure om te bepalen welke poortinstellingen worden gebruikt voor WSUS.  

#### <a name="to-determine-the-port-settings-used-in-iis"></a>Bepalen welke poortinstellingen worden gebruikt in IIS  

 1.  Open IIS-beheer (Internet Information Services) op de WSUS-server.  

 2.  Vouw **Sites**uit, klik met de rechtermuisknop op de website voor de WSUS-server en klik op **Bindingen bewerken**. In het dialoogvenster Sitebindingen worden de waarden voor de HTTP- en HTTPS-poort weergegeven in de kolom **Poort** .


### <a name="configure-ssl-communications-to-wsus"></a>SSL-communicatie naar WSUS configureren  
 U kunt SSL-communicatie configureren op de pagina **Algemeen** van de wizard of op het tabblad **Algemeen** in de eigenschappen van het software-updatepunt.  

 Voor meer informatie over het gebruik van SSL, zie [Beslissen om WSUS te configureren voor gebruik van SSL](../plan-design/plan-for-software-updates.md#BKMK_WSUSandSSL).  

### <a name="wsus-server-connection-account"></a>WSUS-serververbindingsaccount  
 U kunt een account configureren voor gebruik door de siteserver wanneer het verbinding maakt met WSUS dat op het software-updatepunt wordt uitgevoerd. Wanneer u dit account niet configureert, gebruikt de Configuration Manager het computer account voor de site server om verbinding te maken met WSUS. Configureer het WSUS-serververbindingsaccount op de pagina **Proxy- en accountinstellingen** van de wizard of op het tabblad **Proxy- en accountinstellingen** in de eigenschappen van het software-updatepunt.  U kunt het account configureren op verschillende plaatsen van de wizard, afhankelijk van de versie van Configuration Manager die u gebruikt.  

 Zie [accounts die worden gebruikt](../../core/plan-design/hierarchy/accounts.md)voor meer informatie over Configuration Manager-accounts.  

## <a name="synchronization-source"></a>Synchronisatiebron  
 U kunt de synchronisatie bron stroomopwaarts voor synchronisatie van software-updates configureren op de pagina **synchronisatie bron** van de wizard of op het tabblad **synchronisatie-instellingen** in de eigenschappen van software-update punt componenten. Uw opties voor de synchronisatiebron variëren in functie van de site.  

 Gebruik de volgende tabl voor de beschikbare opties wanneer u he software-updatepunt op een site configureert.  

|Site|Beschikbare opties voor synchronisatiebron|  
|----------|----------------------------------------------|  
|-   Centrale beheersite<br />-   Zelfstandige primaire site|-   Synchroniseren vanaf de website Microsoft Update<br />-   Synchroniseren vanaf een gegevensbronlocatie stroomopwaarts<br />-   Niet synchroniseren vanaf Microsoft Update of een gegevensbron stroomopwaarts|  
|-   Extra software-updatepunten op een site<br />-   Onderliggende primaire site<br />-   Secundaire site|-   Synchroniseren vanaf een gegevensbronlocatie stroomopwaarts|  

 De volgende lijst geeft meer informatie over elke optie die u kunt gebruiken als de synchronisatiebron:  

-   **Synchroniseren vanuit Microsoft Update**: gebruik deze instelling om metagegevens van software-updates van Microsoft Update te synchroniseren. De centrale beheersite moet toegang tot het internet hebben; anders zal de synchronisatie mislukken. De instelling is alleen beschikbaar wanneer u het software-updatepunt op een site op het hoogste niveau configureert.  

    > [!NOTE]  
    >  Wanneer zich een firewall tussen het software-updatepunt en internet bevindt, moet de firewall mogelijk worden geconfigureerd om de HTTP- en HTTPS-poorten te accepteren die worden gebruikt voor de WSUS-website. U kunt ook kiezen om de toegang op de firewall te beperken tot beperkte domeinen. Zie [Firewalls configureren](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls)voor meer informatie over het plannen van een firewall die software-updates ondersteunt.  

-   **Synchroniseren vanaf een gegevens bron locatie stroomopwaarts: gebruik deze instelling om meta gegevens van software-updates te synchroniseren vanuit de upstream-synchronisatie bron. <a name="BKMK_wsussync"> </a>** De onderliggende primaire sites en secundaire sites worden automatisch geconfigureerd om de URL van de bovenliggende site voor deze instelling te gebruiken. U kunt de software-updates synchroniseren vanaf een bestaande WSUS-server. Geef een URL op, bijvoorbeeld `https://WSUSServer:8531`, waarbij 8531 de poort is die wordt gebruikt om verbinding te maken met de WSUS-server.  

-   **Niet synchroniseren vanuit Microsoft Update of gegevensbron stroomopwaarts**: gebruik deze instelling om software-updates handmatig te synchroniseren wanneer het software-updatepunt op de site op het hoogste niveau niet is verbonden met internet. Zie de sectie [Software-updates synchroniseren vanaf een niet-verbonden software-updatepunt](synchronize-software-updates-disconnected.md)voor meer informatie.  

> [!NOTE]  
>  Wanneer zich een firewall tussen het software-updatepunt en internet bevindt, moet de firewall mogelijk worden geconfigureerd om de HTTP- en HTTPS-poorten te accepteren die worden gebruikt voor de WSUS-website. U kunt ook kiezen om de toegang op de firewall te beperken tot beperkte domeinen. Zie [Firewalls configureren](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls)voor meer informatie over het plannen van een firewall die software-updates ondersteunt.  

 U kunt ook configureren of u WSUS-rapportage gebeurtenissen op de pagina **synchronisatie bron** van de wizard of op het tabblad **synchronisatie-instellingen** in de eigenschappen van software-update punt componenten wilt maken. Configuration Manager maakt geen gebruik van deze gebeurtenissen. Daarom kiest u doorgaans de standaard instelling **geen WSUS-rapportage gebeurtenissen maken**.  

## <a name="synchronization-schedule"></a>Synchronisatieplanning  
 Configureer de synchronisatieplanning op het tabblad **Synchronisatieplanning** van de wizard of in de eigenschappen van software-updatepuntcomponenten. Deze instelling wordt alleen geconfigureerd op het software-updatepunt op de site op het hoogste niveau.  

 Als u de planning inschakelt, kunt u een terugkerende eenvoudige of aangepaste synchronisatieplanning configureren. Wanneer u een eenvoudige planning configureert, is de start tijd gebaseerd op de lokale tijd voor de computer die de Configuration Manager-console uitvoert op het moment dat u de planning maakt. Wanneer u de start tijd voor een aangepast schema configureert, is dit gebaseerd op de lokale tijd voor de computer waarop de Configuration Manager-console wordt uitgevoerd.  

> [!TIP]  
>  Maak een zodanige planning dat de synchronisatie van de software-updates wordt uitgevoerd met een tijdskader dat geschikt is voor uw omgeving. Een typisch scenario is het instellen van de planning voor de synchronisatie van software-updates om uit te voeren kort na de regelmatige vrijgave van de beveiligingsupdate van Microsoft op de tweede dinsdag van elke maand, die gewoonlijk Patch Dinsdag wordt genoemd. Een ander typisch scenario is het instellen van de planning voor de synchronisatie van software-updates om dagelijks uitgevoerd te worden wanneer u software-updates gebruikt om de Endpoint Protection-definitie en engine-updates te leveren.  

> [!NOTE]  
>  Wanneer u ervoor kiest geen synchronisatie van software-updates op een planning in te schakelen, kunt u software-updates handmatig synchroniseren vanuit het knooppunt **Alle software-updates** of **Software-updategroepen** in de werkruimte Softwarebibliotheek. Zie [software-updates synchroniseren](synchronize-software-updates.md)voor meer informatie.  

## <a name="supersedence-rules"></a>Vervangingsregels  
 Configureer de vervangingsregels op de pagina **Vervangingsregels** van de wizard of op het tabblad **Vervangingsregels** in de eigenschappen van software-updatepuntcomponenten. U kunt de vervangingsregels enkel op de site op het hoogste niveau configureren. Vanaf Configuration Manager versie 1810 kunt u het gedrag van de vervangings regels voor **onderdeel updates** afzonderlijk van **updates zonder onderdelen**opgeven. <!--3098809, 2977644-->

 Op deze pagina kunt u specificeren dat de vervangen software-updates onmiddellijk verlopen zijn, hetgeen voorkomt dat ze worden opgenomen in nieuwe implementaties en de bestaande implementaties markeert om aan te geven dat de vervangen software-updates een of meerdere verlopen software-updates bevatten. U kunt ook een periode opgeven waarna de vervangen software-updates verlopen, zodat u ze nog kunt blijven implementeren. Zie [Supersedence rules](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules)voor meer informatie.  

> [!NOTE]  
>  De pagina **Vervangingsregels** van de wizard is enkel toegankelijk wanneer u het eerste software-updatepunt op de site configureert. Deze pagina wordt niet weergegeven wanneer u aanvullende software-updatepunten installeert.  

## <a name="classifications"></a>Classificaties  
 Configureer de classificatie-instellingen op de pagina **classificaties** van de wizard of op het tabblad **classificaties** in de eigenschappen van software-update punt componenten. Voor meer informatie over software-updateclassificaties, zie[Updateclassificaties](../plan-design/plan-for-software-updates.md#BKMK_UpdateClassifications).  

> [!NOTE]  
>  De pagina **Classificaties** van de wizard is alleen beschikbaar wanneer u het eerste software-updatepunt op de site configureert. Deze pagina wordt niet weergegeven wanneer u aanvullende software-updatepunten installeert.  

> [!TIP]  
>  Wanneer u het software-updatepunt op de site op het hoogste niveau voor het eerst installeert, wis dan alle software-updataclassificaties. Na de initiële synchronisatie van de software-updates configureert u de classificaties vanuit een bijgewerkte lijst, en start u de synchronisatie opnieuw. Deze instelling wordt alleen geconfigureerd op het software-updatepunt op de site op het hoogste niveau.  

## <a name="products"></a>Producten  
 Configureer de product instellingen op de pagina **producten** van de wizard of op het tabblad **producten** in de eigenschappen van software-update punt componenten.  

> [!NOTE]  
>  De pagina **Producten** van de wizard is alleen beschikbaar wanneer u het eerste software-updatepunt op de site configureert. Deze pagina wordt niet weergegeven wanneer u aanvullende software-updatepunten installeert.  

> [!TIP]  
>  Wanneer u het software-updatepunt op de site op het hoogste niveau voor het eerst installeert, wis dan alle producten. Na de initiële synchronisatie van de software-updates configureert u de producten vanuit een bijgewerkte lijst, en start u de synchronisatie opnieuw. Deze instelling wordt alleen geconfigureerd op het software-updatepunt op de site op het hoogste niveau.  

## <a name="languages"></a>Talen  
 Configureer de taal instellingen op de pagina **talen** van de wizard of op het tabblad **talen** in de eigenschappen van software-update punt componenten. Specificeer de talen waarvoor u software-updatebestanden en overzichtsgegevens wilt synchroniseren. De instelling van het **Software-update bestand** is geconfigureerd op elk software-update punt in de Configuration Manager-hiërarchie. De **Overzichtsgegevens**-instellingen worden enkel geconfigureerd op het software-updatepunt op het hoogste niveau. Voor meer informatie raadpleegt u [Talen](../plan-design/plan-for-software-updates.md#BKMK_UpdateLanguages).  

> [!NOTE]  
>  De pagina **Talen** van de wizard is alleen beschikbaar wanneer u het software-updatepunt op de centrale beheersite installeert. U kunt de talen van het Software-updatebestand op onderliggende sites configureren op het tabblad **Talen** in de eigenschappen van software-updatecomponenten.  

## <a name="third-party-updates"></a>Updates van derden
Vanaf Configuration Manager versie 1802 kunt u updates van derden inschakelen voor Configuration Manager-clients. Wanneer u software-updates van derden inschakelt in de eigenschappen van het SUP-onderdeel, wordt door de SUP het handtekening certificaat gedownload dat door WSUS wordt gebruikt voor updates van derden. Deze optie is niet beschikbaar tijdens de installatie van het software-update punt en moet worden geconfigureerd nadat het SUP is geïnstalleerd. Als u de client instellingen voor updates van derden wilt inschakelen, raadpleegt u het artikel [over client instellingen](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates) .

## <a name="next-steps"></a>Volgende stappen
U hebt het software-update punt geïnstalleerd vanaf de bovenste site in uw Configuration Manager-hiërarchie. Herhaal de procedures in dit artikel om het software-update punt op onderliggende sites te installeren.

Als uw software-update punten zijn geïnstalleerd, gaat u naar [software-updates synchroniseren](synchronize-software-updates.md).
