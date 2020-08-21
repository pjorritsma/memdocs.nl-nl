---
title: Beveiliging en privacy voor apps
titleSuffix: Configuration Manager
description: Richt lijnen en aanbevelingen voor beveiliging en privacy bij het beheren van toepassingen in Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e3ceb036180d002956eb0f62348ad317dfce6e7e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695134"
---
# <a name="security-and-privacy-for-application-management-in-configuration-manager"></a>Beveiliging en privacy voor toepassings beheer in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

## <a name="security-guidance-for-application-management"></a>Beveiligings richtlijnen voor toepassings beheer  

### <a name="use-the-software-center-without-the-application-catalog"></a>Software Center gebruiken zonder de Application Catalog

<!--1358309-->

De Silverlight-gebruikers ervaring van de toepassings catalogus wordt niet ondersteund vanaf de huidige branch-versie 1806. Met deze configuratie kunt u de server infrastructuur verminderen die nodig is voor het leveren van toepassingen aan gebruikers.

Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910. Het verminderen van de server infrastructuur vermindert ook de kwets baarheid voor aanvallen.

Gebruik Azure Active Directory en de Cloud beheer gateway om een consistente en veilige toepassings ervaring te bieden voor clients op internet.

Zie [Software Center configureren](plan-for-software-center.md#bkmk_userex)voor meer informatie.

### <a name="use-https-with-the-application-catalog"></a>HTTPS gebruiken met de toepassings catalogus

> [!Important]  
> Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910. Zie [de Application Catalog verwijderen](plan-for-and-configure-application-management.md#bkmk_remove-appcat)voor meer informatie.  

Configureer het Application catalog-website punt en het Application Catalog-webservicepunt om HTTPS-verbindingen te accepteren. Met deze configuratie wordt de server geverifieerd voor gebruikers. De verzonden gegevens zijn beveiligd tegen knoeien en weer gave.

Hulp bij het voor komen van sociale-engineering-aanvallen door gebruikers te trainen om alleen verbinding te maken met vertrouwde websites. Gebruikers informeren over de gevaren van schadelijke websites.

Gebruik niet de huisstijl configuratie opties wanneer u HTTPS niet gebruikt. Deze instellingen tonen de naam van uw organisatie in de Application Catalog als identiteits bewijs.  


### <a name="use-role-separation"></a>Functie scheiding gebruiken

> [!Important]  
> Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910. Zie [de Application Catalog verwijderen](plan-for-and-configure-application-management.md#bkmk_remove-appcat)voor meer informatie.  

Installeer het Application catalog-website punt en het Application Catalog-webservicepunt op afzonderlijke servers. Als er is geknoeid met het website punt, wordt dit gescheiden van het webservicepunt. Dit ontwerp helpt bij het beveiligen van de Configuration Manager-clients en-infra structuur. Deze configuratie is vooral belang rijk als het website punt client verbindingen van het internet accepteert. Het maakt de server kwetsbaar voor aanvallen.  

### <a name="close-browser-windows"></a>Browser vensters sluiten

> [!Important]  
> Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910. Zie [de Application Catalog verwijderen](plan-for-and-configure-application-management.md#bkmk_remove-appcat)voor meer informatie.  

Train gebruikers om het browser venster te sluiten wanneer ze klaar zijn met het gebruik van de toepassings catalogus. Als gebruikers naar een externe website bladeren in hetzelfde browser venster dat ze voor de toepassings catalogus hebben gebruikt, blijft de browser de beveiligings instellingen gebruiken die geschikt zijn voor vertrouwde sites in het intranet.  

### <a name="centrally-specify-user-device-affinity"></a>De gebruikers affiniteit van het apparaat centraal opgeven

Geef hand matig de gebruikers affiniteit van het apparaat op in plaats van het primaire apparaat van gebruikers te laten identificeren. Geen op gebruik gebaseerde configuratie inschakelen.

Houd er rekening mee dat de gegevens die worden verzameld van gebruikers of van het apparaat niet als gezaghebbend worden beschouwd. Als u software implementeert met behulp van affiniteit tussen gebruikers en apparaten die niet door een vertrouwde beheerder wordt opgegeven, kan de software worden geïnstalleerd op computers en voor gebruikers die niet zijn geautoriseerd om die software te ontvangen.  

### <a name="dont-run-deployments-from-distribution-points"></a>Implementaties niet uitvoeren vanaf distributie punten

Configureer altijd dat implementaties inhoud downloaden vanaf distributiepunten, in plaats van uitvoeren vanaf distributiepunten. Wanneer u implementaties configureert om inhoud te downloaden vanaf een distributie punt en lokaal uit te voeren, controleert de Configuration Manager-client de pakket-hash nadat de inhoud is gedownload. De client verwijdert het pakket als de hash niet overeenkomt met de hash in het beleid.

Als u de implementatie configureert om rechtstreeks vanaf een distributie punt te worden uitgevoerd, controleert de Configuration Manager-client de pakket-hash niet. Dit gedrag houdt in dat de Configuration Manager-client software kan installeren waarmee is geknoeid.

Als u implementaties rechtstreeks moet uitvoeren vanaf distributie punten, gebruikt u de minimale NTFS-machtigingen voor de pakketten op de distributie punten. Gebruik ook Internet Protocol Security (IPsec) om het kanaal tussen de client en de distributie punten en tussen de distributie punten en de site server te beveiligen.

### <a name="dont-let-users-interact-with-elevated-processes"></a><a name="bkmk_interact"></a> Laat gebruikers niet werken met verhoogde processen
  
Als u de opties voor **uitvoeren met beheerders rechten** of **installeren voor systeem**inschakelt, kunnen gebruikers niet communiceren met deze toepassingen. Wanneer u een toepassing configureert, kunt u de optie instellen om **gebruikers toe te staan de programma-installatie te bekijken en ermee te werken**. Met deze instelling kunnen gebruikers reageren op eventuele vereiste prompts in de gebruikers interface. Als u de toepassing ook configureert om te worden **uitgevoerd met beheerders rechten**of vanaf versie 1802 **installeren voor systeem**, kan een aanvaller op de computer waarop het programma wordt uitgevoerd de gebruikers interface gebruiken om bevoegdheden te escaleren op de client computer.

Gebruik Program ma's die Windows Installer gebruiken voor Setup en verhoogde bevoegdheden per gebruiker voor software-implementaties waarvoor beheerders referenties zijn vereist. Het installatie programma moet worden uitgevoerd in de context van een gebruiker die geen beheerders referenties heeft. Windows Installer bevoegdheden per gebruiker met verhoogde bevoegdheid bieden de veiligste manier om toepassingen met deze vereiste te implementeren.

### <a name="restrict-whether-users-can-install-software-interactively"></a>Beperken of gebruikers interactief software kunnen installeren

Configureer de **installatie machtigingen** client instelling in de groep **computer agent** . Met deze instelling worden de soorten gebruikers beperkt die software in Software Center kunnen installeren.

Maak bijvoorbeeld een aangepaste clientinstelling met **Installatiemachtigingen** ingesteld op **Alleen beheerders**. Deze client instelling Toep assen op een verzameling van servers. Deze configuratie voor komt dat gebruikers zonder beheerders rechten software op deze servers installeren.  

### <a name="for-mobile-devices-deploy-only-applications-that-are-signed"></a>Implementeer voor mobiele apparaten alleen toepassingen die zijn ondertekend

Implementeer alleen toepassingen voor mobiele apparaten als de code is ondertekend door een certificerings instantie (CA) die door het mobiele apparaat wordt vertrouwd.

Bijvoorbeeld:

- Een toepassing van een leverancier, die is ondertekend door een bekende CA zoals VeriSign.  

- Een interne toepassing die u onafhankelijk van Configuration Manager aanmeldt met behulp van uw interne certificerings instantie.  

- Een interne toepassing die u aanmeldt met behulp van Configuration Manager wanneer u het toepassings type maakt en een handtekening certificaat gebruikt.

### <a name="secure-the-location-of-the-mobile-device-application-signing-certificate"></a>De locatie van het handtekening certificaat van de toepassing voor mobiele apparaten beveiligen

Als u toepassingen voor mobiele apparaten ondertekent met behulp van de **wizard toepassing maken** in Configuration Manager, de locatie van het handtekening certificaat bestand beveiligen en het communicatie kanaal beveiligen. Sla het handtekening certificaat bestand op in een beveiligde map om te helpen beschermen tegen verhoging van bevoegdheden en tegen man-in-the-middle-aanvallen.

Gebruik IPsec tussen de volgende computers:

- De computer waarop de Configuration Manager-console wordt uitgevoerd
- De computer die het handtekening bestand voor het certificaat opslaat
- De computer waarop de bron bestanden van de toepassing worden opgeslagen

U kunt de toepassing ook ondertekenen onafhankelijk van Configuration Manager en voordat u de **wizard toepassing maken**uitvoert.

### <a name="implement-access-controls"></a>Toegangs beheer implementeren

Implementeer toegangs beheer om referentie computers te beveiligen. Wanneer u de detectie methode in een implementatie type configureert door te bladeren naar een referentie computer, moet u ervoor zorgen dat de computer niet is aangetast.

### <a name="restrict-and-monitor-administrative-users"></a>Gebruikers met beheerders rechten beperken en bewaken

Beperk en bewaak de gebruikers met beheerders rechten die u de volgende op rollen gebaseerde beveiligings rollen op toepassings beheer verleent:

- **Toepassingsbeheerder**
- **Toepassingsauteur**
- **Beheerder toepassingsimplementaties**

Zelfs wanneer u op rollen gebaseerd beheer configureert, is het mogelijk dat gebruikers met beheerdersrechten die toepassingen maken en implementeren meer machtigingen hebben dan u beseft. Gebruikers met beheerders rechten die een toepassing maken of wijzigen, kunnen bijvoorbeeld afhankelijke toepassingen selecteren die zich niet in hun beveiligings bereik bevinden.

### <a name="configure-app-v-apps-in-virtual-environments-with-the-same-trust-level"></a>App-V-apps in virtuele omgevingen met hetzelfde vertrouwens niveau configureren

Wanneer u virtuele omgevingen van micro soft Application Virtualization (app-V) configureert, selecteert u toepassingen met hetzelfde vertrouwens niveau in de virtuele omgeving. Omdat toepassingen in een virtuele app-V-omgeving resources kunnen delen, zoals het klem bord, configureert u de virtuele omgeving zo dat de geselecteerde toepassingen hetzelfde vertrouwens niveau hebben.

Zie [virtuele omgevingen van app-V maken](../deploy-use/create-app-v-virtual-environments.md)voor meer informatie.

### <a name="make-sure-macos-apps-are-from-a-trustworthy-source"></a>Controleer of macOS-apps afkomstig zijn van een betrouw bare bron

Als u toepassingen voor macOS-apparaten implementeert, moet u ervoor zorgen dat de bron bestanden afkomstig zijn van een betrouw bare bron. Het hulp programma CMAppUtil valideert de hand tekening van het bron pakket niet. Zorg ervoor dat het pakket afkomstig is van een bron die u vertrouwt. Het hulp programma CMAppUtil kan niet detecteren of er is geknoeid met de bestanden.

### <a name="secure-the-cmmac-file-for-macos-apps"></a>Het cmmac-bestand voor macOS-apps beveiligen

Als u toepassingen implementeert voor macOS-computers, beveiligt u de locatie van het **. cmmac** -bestand. Het CMAppUtil-hulp programma genereert dit bestand en importeert u het vervolgens in Configuration Manager. Dit bestand is niet ondertekend of gevalideerd.

Beveilig het communicatie kanaal wanneer u dit bestand importeert in Configuration Manager. Als u wilt voor komen dat dit bestand wordt geknoeid, slaat u het op in een beveiligde map. Gebruik IPsec tussen de volgende computers:

- De computer waarop de Configuration Manager-console wordt uitgevoerd  
- De computer waarop het **. cmmac** -bestand wordt opgeslagen  

### <a name="use-https-for-web-applications"></a>HTTPS gebruiken voor webtoepassingen

Als u een implementatie type voor een webtoepassing configureert, gebruikt u HTTPS om de verbinding te beveiligen. Als u een webtoepassing implementeert met behulp van een HTTP-koppeling in plaats van een HTTPS-koppeling, kan het apparaat worden omgeleid naar een rogue-server. Gegevens die worden overgedragen tussen het apparaat en de server, kunnen worden gemanipuleerd.


## <a name="security-issues-for-application-management"></a>Beveiligingsproblemen voor toepassingsbeheer  

- Gebruikers met beperkte rechten kunnen bestanden van de clientcache naar de clientcomputer kopiëren .  

     Gebruikers kunnen de client cache lezen, maar er kan niet naar worden geschreven. Met leesmachtigingen kan een gebruiker toepassingsinstallatiebestanden van een computer naar een andere computer kopiëren.  

- Gebruikers met beperkte rechten kunnen bestanden wijzigen die de geschiedenis van de software-implementatie op de client computer vastleggen.  

     Omdat de gegevens van de toepassings geschiedenis niet zijn beveiligd, kan een gebruiker bestanden wijzigen die rapporteren of een toepassing is geïnstalleerd.  

- App-V-pakketten zijn niet ondertekend.  

     App-V-pakketten in Configuration Manager ondertekenen niet ondersteunen. Digitale hand tekeningen verifiëren dat de inhoud afkomstig is van een vertrouwde bron en niet is gewijzigd tijdens de overdracht. Er is geen beperking voor dit beveiligings probleem. Volg de beveiligings best practice om de inhoud van een vertrouwde bron en van een veilige locatie te downloaden.  

- Gepubliceerde App-V-toepassingen kunnen door alle gebruikers op de computer worden geïnstalleerd.  

     Wanneer een app-V-toepassing op een computer wordt gepubliceerd, kunnen alle gebruikers die zich aanmelden bij die computer de toepassing installeren. U kunt de gebruikers niet beperken die de toepassing kunnen installeren nadat deze is gepubliceerd.  


## <a name="certificates-for-microsoft-silverlight-5-and-elevated-trust-mode-required-for-the-application-catalog"></a><a name="BKMK_CertificatesSilverlight5"></a> Certificaten voor micro soft Silverlight 5 en verhoogde vertrouwens modus vereist voor de Application Catalog  

> [!Important]  
> Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910. Zie [de Application Catalog verwijderen](plan-for-and-configure-application-management.md#bkmk_remove-appcat)voor meer informatie.  

Voor Configuration Manager-clients versie 1710 en eerder is micro soft Silverlight 5 vereist, die moet worden uitgevoerd in verhoogde vertrouwens modus voor gebruikers om software te installeren vanuit de toepassings catalogus. Silverlight-toepassingen worden standaard uitgevoerd in gedeeltelijke vertrouwensmodus om te voorkomen dat toepassingen toegang hebben tot gebruikersgegevens. Als dat nog niet is gebeurd, installeert Configuration Manager automatisch micro soft Silverlight 5 op clients. Configuration Manager stelt de computer agent standaard **toestaan dat Silverlight-toepassingen worden uitgevoerd in verhoogde vertrouwens modus** client instelling op **Ja**. Met deze instelling kunnen ondertekende en vertrouwde Silverlight-toepassingen verhoogde vertrouwde modus aanvragen.  

Wanneer u de site systeemrol Application catalog-website punt installeert, installeert de client ook een micro soft-handtekening certificaat in het certificaat archief Vertrouwde uitgevers van de computer op elke Configuration Manager-client computer. Silverlight-toepassingen die zijn ondertekend door dit certificaat, worden uitgevoerd in de verhoogde vertrouwens modus, op welke computers software moet worden geïnstalleerd vanuit de toepassings catalogus. Configuration Manager dit handtekening certificaat automatisch beheert. Als u de service continuïteit wilt verhogen, moet u dit micro soft-handtekening certificaat niet hand matig verwijderen of verplaatsen.  

> [!WARNING]  
> Wanneer deze optie is ingeschakeld, worden alle Silverlight-toepassingen die zijn ondertekend door certificaten in het certificaat archief van vertrouwde uitgevers in het computer archief of in het gebruikers archief, in verhoogde vertrouwens modus uitgevoerd wanneer de client instelling **toestaan dat Silverlight-toepassingen worden uitgevoerd in verhoogde vertrouwens modus** . De client instelling kan verhoogde vertrouwens modus niet speciaal inschakelen voor de Configuration Manager Application Catalog of voor het certificaat archief Vertrouwde uitgevers in het computer archief. Als malware een Rogue-certificaat in het archief met vertrouwde uitgevers toevoegt, kan schadelijke software met een eigen Silverlight-toepassing nu ook worden uitgevoerd in verhoogde vertrouwens modus.  

Als u de instelling **toestaan dat Silverlight-toepassingen worden uitgevoerd in verhoogde vertrouwens modus** is ingesteld op **Nee**, wordt het micro soft-handtekening certificaat niet door clients verwijderd.  

Zie [Trusted Applications (vertrouwde toepassingen](/previous-versions/windows/silverlight/dotnet-windows-silverlight/ee721083\(v=vs.95\))) voor meer informatie over vertrouwde toepassingen in Silverlight.  


## <a name="privacy-information-for-application-management"></a> Privacyinformatie voor toepassingsbeheer  

Met toepassings beheer kunt u elke toepassing, elk programma of elk script uitvoeren op elke client in de hiërarchie. Configuration Manager heeft geen controle over de typen toepassingen, Program ma's of scripts die u uitvoert of het type informatie dat ze verzenden. Tijdens het toepassings implementatie proces kan Configuration Manager informatie verzenden waarmee het apparaat en de aanmeldings accounts tussen clients en servers worden geïdentificeerd.  

Configuration Manager onderhoudt status informatie over het software-implementatie proces. Informatie over software-implementatie status is niet versleuteld tijdens de verzen ding, tenzij de client communiceert met behulp van HTTPS. De status informatie wordt niet in een versleutelde vorm opgeslagen in de-data base.  

Het gebruik van Configuration Manager toepassings installatie op afstand, interactief of op de achtergrond installeren van software op clients is mogelijk onderhevig aan software licentie voorwaarden voor die software. Dit gebruik staat los van de Software licentievoorwaarden voor Configuration Manager. Controleer en ga altijd akkoord met de licentie voorwaarden voor software voordat u software implementeert met behulp van Configuration Manager.  

Configuration Manager verzamelt diagnostische en gebruiks gegevens over toepassingen, die door micro soft worden gebruikt om toekomstige releases te verbeteren. Zie [diagnostiek en gebruiks gegevens](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)voor meer informatie.

Toepassings implementatie vindt niet standaard plaats en vereist verschillende configuratie stappen.  

De volgende functies helpen een efficiënte software-implementatie:

- **Gebruikers affiniteit apparaat** wijst een gebruiker toe aan apparaten. Een Configuration Manager-beheerder implementeert software aan een gebruiker. De-client installeert de software automatisch op een of meer computers die de gebruiker het vaakst gebruikt.  

- **Software Center** wordt automatisch op een apparaat geïnstalleerd wanneer u de Configuration Manager-client installeert. Gebruikers kunnen instellingen wijzigen, zoeken naar software vanuit software Center en deze installeren.  

- De **toepassings catalogus** is een website waarmee gebruikers software kunnen aanvragen om te installeren.  

    > [!Important]  
    > Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910. Zie [de Application Catalog verwijderen](plan-for-and-configure-application-management.md#bkmk_remove-appcat)voor meer informatie.  

### <a name="user-device-affinity-privacy-information"></a><a name="bkmk_privacy-uda"></a> Privacygegevens van affiniteit van gebruiker met apparaat

- Configuration Manager kan informatie verzenden tussen clients en beheer punt site systemen. De informatie kan de computer en het aanmeldings account en het overzichts gebruik voor aanmeldings accounts identificeren.  

- De gegevens die worden verzonden tussen de client en de server zijn niet versleuteld, tenzij het beheer punt zodanig is geconfigureerd dat clients moeten communiceren met behulp van HTTPS.  

- De informatie over het gebruik van de computer en het aanmeldings account, die wordt gebruikt om een gebruiker toe te wijzen aan een apparaat, wordt opgeslagen op client computers, verzonden naar beheer punten en vervolgens opgeslagen in de Configuration Manager-Data Base. De oude informatie wordt standaard na 90 dagen van de database verwijderd. U kunt het verwijderingsgedrag configureren door de siteonderhoudstaak **Verouderde gegevens apparaataffiniteit voor gebruikers verwijderen** in te stellen.  

- Configuration Manager houdt status informatie over de affiniteit van gebruikers apparaten. Status informatie is tijdens de verzen ding niet versleuteld, tenzij clients zijn geconfigureerd om te communiceren met beheer punten met behulp van HTTPS. Status informatie wordt niet in een versleutelde vorm opgeslagen in de-data base.  

- Informatie over het gebruik van computers en aanmeld gegevens die wordt gebruikt om de affiniteit van gebruikers en apparaten in te richten, is altijd ingeschakeld. Gebruikers en gebruikers met beheerders rechten kunnen informatie over de affiniteit van gebruikers apparaten opgeven.  

### <a name="software-center-privacy-information"></a><a name="bkmk_privacy-userex"></a> Privacy-informatie voor Software Center

- Met Software Center kan de Configuration Manager-beheerder elke toepassing of elk programma of script publiceren zodat gebruikers ze kunnen uitvoeren. Configuration Manager heeft geen controle over de typen Program ma's of scripts die zijn gepubliceerd in de catalogus of het type informatie dat ze verzenden.  

- Configuration Manager kan informatie verzenden tussen clients en het beheer punt. De informatie kan de computer-en aanmeldings accounts identificeren. De gegevens die worden verzonden tussen de client en servers, worden niet versleuteld, tenzij u het beheer punt zo configureert dat clients verbinding kunnen maken met behulp van HTTPS.  

- De informatie over de goedkeurings aanvraag voor toepassingen wordt opgeslagen in de Configuration Manager-Data Base. Aanvragen die worden geannuleerd of geweigerd en de bijbehorende geschiedenis vermeldingen van de aanvraag worden standaard na 30 dagen verwijderd. U kunt het verwijderingsgedrag configureren door de siteonderhoudstaak **Verouderde gegevens toepassingsaanvraag verwijderen** in te stellen. Goedkeurings aanvragen voor toepassingen die zijn goedgekeurd en status in behandeling, worden nooit verwijderd.  

- Software Center wordt automatisch geïnstalleerd wanneer u de Configuration Manager-client op een apparaat installeert.  

### <a name="application-catalog-privacy-information"></a>Informatie over Application Catalog-privacy

> [!Important]  
> Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910. Zie [de Application Catalog verwijderen](plan-for-and-configure-application-management.md#bkmk_remove-appcat)voor meer informatie.  

- De toepassings catalogus wordt niet standaard geïnstalleerd. Deze installatie vereist verschillende configuratiestappen.  

- Met de toepassings catalogus kan de Configuration Manager-beheerder elke toepassing of elk programma of script publiceren dat gebruikers kunnen uitvoeren. Configuration Manager heeft geen controle over de typen Program ma's of scripts die zijn gepubliceerd in de catalogus of het type informatie dat ze verzenden.  

- Configuration Manager kan informatie verzenden tussen clients en de Application Catalog-site systeem rollen. De informatie kan de computer-en aanmeldings accounts identificeren. De gegevens die worden verzonden tussen de client en servers, worden niet versleuteld, tenzij deze site systeem rollen zodanig zijn geconfigureerd dat clients verbinding kunnen maken met behulp van HTTPS.