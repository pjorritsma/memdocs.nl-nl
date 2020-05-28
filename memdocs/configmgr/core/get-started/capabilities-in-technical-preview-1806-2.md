---
title: Technical Preview 1806,2
titleSuffix: Configuration Manager
description: Meer informatie over nieuwe functies die beschikbaar zijn in de Configuration Manager Technical Preview versie 1806,2.
ms.date: 06/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3af2a69d-30e7-4dce-832d-82b7a1c082f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b7643c73d2e9dad00e926bdc3db905016c45860a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905220"
---
# <a name="capabilities-in-technical-preview-18062-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1806,2 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1806,2. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Technical Preview-site. 

Raadpleeg het artikel [Technical Preview](technical-preview.md) voordat u deze update installeert. In dit artikel wordt u vertrouwd met de algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->

## <a name="known-issues-in-this-technical-preview"></a>Bekende problemen in deze Technical Preview

### <a name="clients-dont-automatically-update"></a><a name="ki_sqlncli"></a>Clients worden niet automatisch bijgewerkt
<!--518760-->
Bij het bijwerken naar versie 1806,2 werkt de site ook de SQL Native Client bij, waardoor het opnieuw opstarten van de site server kan worden veroorzaakt. Deze vertraging leidt ertoe dat bepaalde bestanden niet worden bijgewerkt, wat van invloed is op automatische client upgrade.

#### <a name="workarounds"></a>Tijdelijke oplossingen
U kunt dit probleem voor komen door de SQL Native Client hand matig bij te *werken voordat u Configuration Manager bijwerkt* naar versie 1806,2. Zie de [nieuwste onderhouds update voor SQL Server 2012 native client](https://www.microsoft.com/download/details.aspx?id=50402)voor meer informatie.

Als u uw site al hebt bijgewerkt, werkt automatische client upgrade en client push niet. U moet clients bijwerken om de meeste nieuwe functies volledig te testen. Werk uw Technical Preview-clients hand matig bij met het volgende proces:  

1. Zoek de client bron bestanden in de map **CMUClient** van de installatiemap van Configuration Manager op de site server. Bijvoorbeeld: `C:\Program Files\Configuration Manager\CMUClient`  

2. Kopieer de volledige map CMUClient naar het client apparaat. Bijvoorbeeld: `C:\Temp\CMUClient`  

    Deze locatie kan een netwerk share zijn die toegankelijk is vanaf de-clients.  

3. Voer de volgende opdracht regel uit vanaf een opdracht prompt met verhoogde bevoegdheid:`C:\Temp\CMUClient\ccmsetup.exe /source:C:\Temp\CMUClient`  

Gebruik hetzelfde proces als u een nieuwe client installeert in uw Technical Preview versie 1806,2-site. 

> [!Important]  
> Gebruik niet de `/MP` opdracht regel parameter in dit scenario. Deze para meter heeft voor rang boven `/source` en zorgt ervoor dat ccmsetup client inhoud downloadt van het beheer punt of distributie punt.
> 
> Opdracht regel eigenschappen, zoals SMSSITECODE of CCMLOGLEVEL, zijn OK voor gebruik, maar zijn niet nodig bij het upgraden van een bestaande client. 


### <a name="version-18062-shows-version-1806-in-about-configuration-manager"></a><a name="ki_version"></a>Versie 1806,2 toont versie 1806 in about Configuration Manager
<!--518148-->
Als u na de upgrade naar Technical Preview versie 1806,2 het venster **over Configuration Manager** opent in de linkerbovenhoek van de console, wordt nog steeds **versie 1806**weer gegeven. 

#### <a name="workaround"></a>Tijdelijke oplossing
Gebruik de eigenschap **site versie** om het verschil te bepalen tussen 1806 en 1806,2:

| Site versie  | Versie
|---------|---------|
| 5,0.**8672**. 1000 | 1806 |
| 5,0.**8685**. 1000 | 1806,2 |
 


</br>

**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  


## <a name="improvements-to-phased-deployments"></a><a name="bkmk_pod"></a>Verbeteringen in gefaseerde implementaties

Deze release bevat de volgende verbeteringen in [gefaseerde implementaties](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md):
- [Status van gefaseerde implementatie](#bkmk_pod-monitor)
- [Gefaseerde implementatie van toepassingen](#bkmk_pod-app)
- [Geleidelijke implementatie tijdens gefaseerd implementeren](#bkmk_pod-throttle)


### <a name="phased-deployment-status"></a><a name="bkmk_pod-monitor"></a>Status van gefaseerde implementatie
<!--1358577-->
Gefaseerde implementaties hebben nu een systeem eigen bewakings ervaring. Selecteer een gefaseerde implementatie in het knoop punt **implementaties** in de werk ruimte **bewaking** en klik vervolgens op **status van gefaseerde implementatie** in het lint.

![Dash board voor de fase van de implementatie status met de status van twee fasen](media/1358577-phased-deployment-status.png)

Dit dash board bevat de volgende informatie voor elke fase in de implementatie:  

- **Totaal aantal apparaten**: hoeveel apparaten zijn gericht op deze fase.  

- **Status**: de huidige status van deze fase. Elke fase kan een van de volgende statussen hebben:  

    - **Implementatie gemaakt**: de gefaseerde implementatie heeft een implementatie van de software voor deze fase gemaakt. Clients zijn actief gericht op deze software.  

    - **Wachten**: de vorige fase heeft nog niet de criteria voor het slagen van de implementatie bereikt om door te gaan naar deze fase.  

    - **Onderbroken**: een beheerder heeft de implementatie onderbroken.  

- **Voortgang**: de implementatie statussen met kleur code van clients. Bijvoorbeeld: geslaagd, in voortgang, fout, niet voldaan aan vereisten en onbekend. 


#### <a name="known-issue"></a>Bekend probleem
In het dash board met de status van de fase van de implementatie kunnen meerdere rijen voor dezelfde fase worden weer gegeven.<!--518510-->


### <a name="phased-deployment-of-applications"></a><a name="bkmk_pod-app"></a>Gefaseerde implementatie van toepassingen
<!--1358147-->
Gefaseerde implementaties maken voor toepassingen. Met gefaseerde implementaties kunt u een gecoördineerde, geordende implementatie van software organiseren op basis van aanpas bare criteria en groepen.

Ga in de Configuration Manager-console naar de **software bibliotheek**, vouw **toepassings beheer**uit en selecteer **toepassingen**. Selecteer een toepassing en klik vervolgens op **gefaseerde implementatie maken** op het lint. 

Het gedrag van een gefaseerde implementatie van een toepassing is hetzelfde als voor taken reeksen. Zie voor meer informatie [gefaseerde implementaties maken voor een taken reeks](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md).

#### <a name="prerequisite"></a>Vereiste
Distribueer de inhoud voor de toepassing naar een distributie punt voordat u de gefaseerde implementatie maakt.<!--518293-->

#### <a name="known-issue"></a>Bekend probleem
U kunt geen fasen voor een toepassing hand matig maken. De wizard maakt automatisch twee fasen voor toepassings implementaties.


### <a name="gradual-rollout-during-phased-deployments"></a><a name="bkmk_pod-throttle"></a>Geleidelijke implementatie tijdens gefaseerd implementeren
<!--1358578-->
Tijdens een gefaseerde implementatie kan de implementatie in elke fase nu geleidelijk plaatsvinden. Dit gedrag helpt bij het oplossen van problemen met de implementatie en vermindert de belasting van het netwerk, veroorzaakt door de distributie van inhoud naar clients. De site kan geleidelijk de software beschikbaar maken, afhankelijk van de configuratie van elke fase. Elke client in een fase heeft een deadline die relatief is ten opzichte van de tijd dat de software beschikbaar is. Het tijd venster tussen de beschik bare tijd en deadline is hetzelfde voor alle clients in een fase. 

Wanneer u een gefaseerde implementatie maakt en hand matig een fase configureert, op de pagina **fase-instellingen** van de wizard fase toevoegen of op de pagina **instellingen** van de wizard gefaseerde implementatie maken, configureert u de optie: **deze software wordt gedurende deze periode geleidelijk beschikbaar (in dagen)**. De standaard waarde van deze instelling is **0**, dus de implementatie wordt standaard niet beperkt.

> [!Note]  
> Deze optie is momenteel alleen beschikbaar voor gefaseerde implementaties van taken reeksen.  



## <a name="support-for-new-windows-app-package-formats"></a><a name="bkmk_msix"></a>Ondersteuning voor nieuwe Windows-app-pakket indelingen
<!--1357427-->
Configuration Manager ondersteunt nu de implementatie van nieuwe indelingen van Windows 10 app package (. msix) en app-bundel (. msixbundle). De nieuwste Preview-versies van [Windows Insider](https://insider.windows.com/) ondersteunen momenteel deze nieuwe indelingen.

Ga voor een overzicht van MSIX naar [een](https://docs.microsoft.com/archive/blogs/sgern/a-closer-look-at-msix)meer informatie over MSIX.

Zie voor meer informatie over het maken van een nieuwe MSIX-app [MSIX-ondersteuning geïntroduceerd in Insider Build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).

### <a name="prerequisites"></a>Vereisten
- Een Windows 10-client met ten minste Windows Insider preview build 17682
- Een Windows-app-pakket in de MSIX-indeling

### <a name="try-it-out"></a>Probeer het nu!
Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

1. [Maak een toepassing](../../apps/deploy-use/create-applications.md)In de Configuration Manager-console. 
2. Selecteer het installatie bestands **type** van de toepassing als **Windows-app-pakket ( \* . appx, \* . appxbundle, \* . msix, \* . msixbundle)**.
3. [Implementeer de toepassing](../../apps/deploy-use/deploy-applications.md) naar de client met de meest recente preview-versie van Windows Insider.



## <a name="improvement-to-client-push-security"></a><a name="bkmk_client-push"></a>Verbetering van client push beveiliging
<!--1358204-->
Wanneer u de [client push](../clients/deploy/plan/client-installation-methods.md#client-push-installation) methode voor het installeren van de Configuration Manager-client gebruikt, maakt de site server een externe verbinding met de client om de installatie te starten. Vanaf deze release kan de site Kerberos wederzijdse verificatie vereisen door geen terugval op NTLM toe te staan voordat de verbinding tot stand wordt gebracht. Deze verbetering helpt bij het beveiligen van de communicatie tussen de server en de client. 

Afhankelijk van uw beveiligings beleid is het mogelijk dat uw omgeving al een voor keur heeft of Kerberos boven oudere NTLM-verificatie vereist. Zie de [instelling Windows-beveiligings beleid](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations)voor het beperken van NTLM voor meer informatie over de beveiligings overwegingen van deze verificatie protocollen.


### <a name="prerequisite"></a>Vereiste

Als u deze functie wilt gebruiken, moeten clients zich in een vertrouwde Active Directory-forest bevinden. Kerberos in Windows is afhankelijk van Active Directory voor wederzijdse verificatie. 


### <a name="try-it-out"></a>Probeer het nu!

Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

Wanneer u de site bijwerkt, blijft het bestaande gedrag behouden. Zodra u de eigenschappen van de push installatie van de client hebt *geopend* , wordt de Kerberos-controle automatisch ingeschakeld door de site. Indien nodig kunt u de verbinding toestaan om een minder veilige NTLM-verbinding te gebruiken. dit wordt niet aanbevolen. 

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer **sites**. Selecteer de doel site. Klik in het lint op **instellingen voor client installatie** en selecteer **client push installatie**.  

2. De site heeft nu de Kerberos-controle ingeschakeld voor client push. Klik op **OK** om het venster te sluiten.  

3. Ga indien nodig voor uw omgeving naar de Push-client installatie venster Eigenschappen op het tabblad **Algemeen** de optie voor het **toestaan van verbinding met NTLM**toe. Deze optie is standaard uitgeschakeld. 



## <a name="management-insights-for-proactive-maintenance"></a><a name="bkmk_insights"></a>Management Insights voor proactieve onderhoud
<!--1352184,et al-->
Er zijn extra beheer inzichten beschikbaar in deze versie om mogelijke configuratie problemen te markeren. Controleer de volgende regels in de nieuwe **proactieve onderhouds** groep:  

- **Ongebruikte configuratie-items**: configuratie-items die geen deel uitmaken van een configuratie basislijn en ouder zijn dan 30 dagen.  

- **Ongebruikte opstart installatie kopieën**: er wordt niet naar opstart installatie kopieën verwezen voor het opstarten van de PXE-opstart bewerking of de taken reeks  

- **Grens groepen zonder toegewezen site systemen**: als u geen site systemen hebt toegewezen, kunnen grens groepen alleen worden gebruikt voor site toewijzing.  

- **Grens groepen zonder leden**: grens groepen zijn niet van toepassing op site toewijzing of het opzoeken van inhoud als ze geen leden hebben.  

- **Distributie punten die geen inhoud leveren aan clients**: distributie punten die in de afgelopen 30 dagen geen inhoud hebben aangeboden aan clients. Deze gegevens zijn gebaseerd op rapporten van clients van hun download geschiedenis.  

- **Verlopen updates gevonden**: verlopen updates zijn niet van toepassing op implementatie.   



## <a name="transition-mobile-apps-workload-for-co-managed-devices"></a><a name="bkmk_comgmt"></a>De werk belasting van mobiele apps voor gezamenlijk beheerde apparaten door lopen
<!--1357892-->
Beheer mobiele apps met Microsoft Intune terwijl u Configuration Manager kunt gebruiken om Windows-bureaublad toepassingen te implementeren. Als u de werk belasting van moderne Apps wilt door lopen, gaat u naar de pagina met eigenschappen voor co-beheer. Verplaats de schuif regelaar van Configuration Manager naar pilot of all. 

Nadat u deze werk belasting hebt overgezet, zijn alle beschik bare apps die zijn geïmplementeerd vanuit intune, beschikbaar in de Bedrijfsportal. Apps die u vanaf Configuration Manager implementeert, zijn beschikbaar in Software Center. 

Raadpleeg voor meer informatie de volgende artikelen:  

- [Co-beheer voor Windows 10-apparaten](../../comanage/overview.md)  

- [Wat is Microsoft Intune-appbeheer?](https://docs.microsoft.com/intune/app-management)  



## <a name="boundary-group-options-for-peer-downloads"></a><a name="bkmk_bgoptions"></a>Opties voor grens groepen voor het downloaden van peers
<!--1356193-->
Grens groepen bevatten nu aanvullende instellingen om u meer controle te geven over de distributie van inhoud in uw omgeving. Deze release voegt de volgende opties toe:  

- **Peer-down loads in deze grens groep toestaan**: deze instelling is standaard ingeschakeld. Het beheer punt biedt clients een lijst met inhouds locaties die peer bronnen bevatten. <!--This setting also affects applying Group IDs for Delivery Optimization.518268-->  

    Er zijn twee veelvoorkomende scenario's waarin u deze optie kunt uitschakelen:  

    - Als u een grens groep hebt die grenzen bevat van geografisch verspreide locaties, zoals een VPN. Twee clients kunnen zich in dezelfde grens groep bevinden omdat ze zijn verbonden via VPN, maar op een groot aantal verschillende locaties die niet geschikt zijn voor het delen van inhoud in de peer.  

    - Als u een enkele grote grens groep gebruikt voor site toewijzing die niet verwijst naar een distributie punt.  

- **Tijdens het downloaden van de peer gebruikt u alleen peers binnen hetzelfde subnet**: deze instelling is afhankelijk van de hierboven beschreven. Als u deze optie inschakelt, wordt het beheer punt alleen opgenomen in de inhouds locatie lijst peer bronnen die zich in hetzelfde subnet bevinden als de client.

    Algemene scenario's voor het inschakelen van deze optie:

    - Het ontwerp van de grens groep voor inhouds distributie bevat één grote grens groep die andere kleinere grens groepen overlapt. Met deze nieuwe instelling bevat de lijst met inhouds bronnen die het beheer punt aan clients levert alleen peer bronnen uit hetzelfde subnet.

    - U hebt één grote grens groep voor alle externe kantoor locaties. Als u deze optie inschakelt, delen clients alleen inhoud in het subnet op de externe kantoor locatie, in plaats van een risico op het delen van inhoud tussen locaties.


### <a name="known-issue"></a>Bekend probleem
Als de peer-bron-client meer dan één IP-adres heeft (IPv4, IPv6 of beide), werkt peer-caching niet. De nieuwe optie, **tijdens het downloaden van peers, gebruikt alleen peers binnen hetzelfde subnet**en heeft geen effect als de peer bron meer dan één IP-adres heeft.<!--518661-->   



## <a name="third-party-software-updates-support-for-custom-catalogs"></a><a name="bkmk_3pupdate"></a>Ondersteuning van software-updates van derden voor aangepaste catalogi
<!--1358714-->
In deze release wordt de ondersteuning voor software-updates van derden verder herhaald als gevolg van uw [UserVoice-feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co). [Technical Preview versie 1806](capabilities-in-technical-preview-1806.md#bkmk-3pupdate) biedt ondersteuning voor *partner catalogi*, die geregistreerde catalogi van software leveranciers zijn. Catalogi die u levert, die niet bij micro soft zijn geregistreerd, worden *aangepaste catalogi*genoemd. Aangepaste catalogi toevoegen in de Configuration Manager-console.  


### <a name="prerequisites"></a>Vereisten 

- [Software-updates](capabilities-in-technical-preview-1806.md#bkmk-3pupdate)van derden instellen. Fase 1 volt ooien: de functie inschakelen en instellen.   

- Een digitaal ondertekende aangepaste catalogus die digitaal ondertekende software-updates bevat.  

- De beheerder heeft de volgende machtigingen nodig:  

    - Site: maken, wijzigen  


### <a name="try-it-out"></a>Probeer het nu!

Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **software-updates**uit en selecteer het knoop punt **Software-update catalogi** van derden. Klik op **aangepaste catalogus toevoegen** op het lint.  

2. Geef op de pagina **Algemeen** de volgende gegevens op:  

    - **Download-URL**: een geldig https-adres van de aangepaste catalogus.  

    - **Uitgever**: de naam van de organisatie die de catalogus publiceert.  

    - **Naam**: de naam van de catalogus die in de Configuration Manager-console moet worden weer gegeven.  

    - **Beschrijving**: een beschrijving van de catalogus.  

    - **Ondersteunings-URL** (optioneel): een geldig https-adres van een website om hulp te krijgen bij de catalogus.  

    - **Ondersteunings contact** (optioneel): Neem contact op met informatie om hulp te krijgen bij de catalogus.  

3. Voltooi de wizard. De wizard voegt de nieuwe catalogus toe aan een afgemelde status.  

4. Abonneer u op de aangepaste catalogus met behulp van de bestaande actie **Abonneren op catalogus** . Zie voor meer informatie [fase 2: abonneren op een catalogus van derden en updates synchroniseren](capabilities-in-technical-preview-1806.md#phase-2-subscribe-to-a-third-party-catalog-and-sync-updates).  

> [!Note]  
> U kunt geen catalogi met dezelfde download-URL toevoegen en u kunt geen catalogus eigenschappen bewerken. Als u onjuiste eigenschappen voor een aangepaste catalogus opgeeft, verwijdert u de catalogus voordat u deze opnieuw toevoegt.  


#### <a name="unsubscribe-from-a-catalog"></a>Afmelden bij een catalogus
Als u zich wilt afmelden voor een catalogus, selecteert u de gewenste catalogus in de lijst en klikt u op **catalogus afmelden** in het lint. Als u zich afmeldt bij een catalogus, worden de volgende acties en gedragingen uitgevoerd: 
- De site stopt met het synchroniseren van nieuwe updates 
- De site blokkeert de gekoppelde certificaten voor catalogus ondertekening en update-inhoud. 
- Bestaande updates worden niet verwijderd, maar u kunt ze mogelijk niet publiceren of implementeren.

#### <a name="delete-a-custom-catalog"></a>Een aangepaste catalogus verwijderen
Aangepaste catalogussen verwijderen uit hetzelfde knoop punt van de-console. Selecteer een aangepaste catalogus in de status *unsubscribed* en klik op **aangepaste catalogus verwijderen**. Als u zich al hebt geabonneerd op de catalogus, moet u zich eerst afmelden voordat u deze verwijdert. U kunt geen partner catalogi verwijderen. Als u een aangepaste catalogus verwijdert, wordt deze verwijderd uit de lijst met catalogi. Deze actie is niet van invloed op software-updates die u hebt gepubliceerd op het software-update punt.


### <a name="known-issue"></a>Bekend probleem
De Verwijder actie voor aangepaste catalogi wordt grijs weer gegeven, zodat u geen aangepaste catalogi kunt verwijderen uit de-console. Gebruik het hulp programma **WBEMTest** op de site server om dit probleem op te lossen. Query voor het exemplaar dat u wilt verwijderen met de naam of down load-URL, bijvoorbeeld: `select * from SMS_ISVCatalog where DownloadURL="http://www.contoso.com/catalog.cab"` . Selecteer in het venster query resultaten het object en klik op **verwijderen**.<!--518676-->  



## <a name="improvements-to-cloud-management-features"></a><a name="bkmk_cloud"></a>Verbeteringen in de functies voor Cloud beheer

Deze release bevat de volgende verbeteringen:  

- De volgende functies ondersteunen nu het gebruik van de Azure-Cloud voor de Amerikaanse overheid:<!--511980-->  

    - Onboarding van de site voor **Cloud beheer** via [Azure-Services](../servers/deploy/configure/azure-services-wizard.md)  

    - Een [Cloud beheer gateway met Azure Resource Manager](../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager) implementeren  

    - Een [distributie punt in de Cloud implementeren met Azure Resource Manager](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)  

- Klanten gebruiken Windows auto pilot om Windows 10 in te richten op apparaten die zijn toegevoegd aan Azure Active Directory die zijn verbonden met het on-premises netwerk. Als u de Configuration Manager-client op deze apparaten wilt installeren of upgraden, hebt u een Cloud distributiepunt of een on-premises distributie punt niet nodig om **clients in staat te stellen anoniem verbinding te maken**. Schakel in plaats daarvan de site optie in om door **Configuration Manager gegenereerde certificaten te gebruiken voor HTTP-site systemen**, waarmee een client die lid is van een Cloud, kan communiceren met een on-premises distributie punt met http-functionaliteit. Zie [verbeterde beveiligde client communicatie](https://docs.microsoft.com/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications)voor meer informatie.<!--515854-->  



## <a name="new-software-updates-compliance-report"></a><a name="bkmk_report"></a>Rapport voor naleving van nieuwe software-updates
<!--1357775-->
Het weer geven van rapporten voor de compatibiliteit van software-updates bevat traditioneel gegevens van clients die recent geen contact hebben gemaakt met de site. Met een nieuw rapport kunt u de compatibiliteits resultaten voor een specifieke software-update groep filteren op ' gezonde ' clients. In dit rapport wordt de realistischere compatibiliteits status weer gegeven van de actieve clients in uw omgeving. 
 
Als u het rapport wilt weer geven, gaat u naar de werk ruimte **bewaking** , vouwt u **rapportage**uit, vouwt u **rapporten**uit, vouwt u **software-updates-A compliance**uit en selecteert u **naleving 9-algemene status en naleving**. Geef de **Update groep**, de naam van de **verzameling**en de status van de **client** op.

Het rapport bevat de volgende onderdelen:
- **Goede clients versus totaal aantal clients**: dit staaf diagram vergelijkt de "gezonde" clients die in de opgegeven tijds periode hebben gecommuniceerd met de site ten opzichte van het totale aantal clients in de opgegeven verzameling.
- **Overzicht van naleving**: in dit cirkel diagram wordt de algemene compatibiliteits status weer gegeven voor de specifieke software-update groep op actieve clients in de opgegeven verzameling.
- **Top 5 niet-compatibel met artikel-id**: in dit staaf diagram worden de vijf meest voorkomende software-updates in de opgegeven groep weer gegeven die niet compatibel zijn op actieve clients in de opgegeven verzameling.
- De onderkant van het rapport is een tabel met meer details, waarin de software-updates in de opgegeven groep worden weer gegeven.



## <a name="next-steps"></a>Volgende stappen
Zie [Technical Preview voor Configuration Manager voor](technical-preview.md)meer informatie over het installeren of bijwerken van de technische preview-vertakking.    
