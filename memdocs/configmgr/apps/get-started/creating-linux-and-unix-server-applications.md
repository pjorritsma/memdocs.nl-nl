---
title: Linux- en UNIX-servertoepassingen maken
titleSuffix: Configuration Manager
description: Bekijk welke overwegingen u moet meenemen wanneer u toepassingen voor Linux-en UNIX-apparaten maakt en implementeert.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 79cd131a-1a24-4751-87c8-7f275e45d847
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3f5d0cfb930e6d1b8cf4cd6dfb0eabfa38ddab16
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075775"
---
# <a name="create-linux-and-unix-server-applications-with-configuration-manager"></a>Linux-en UNIX-server toepassingen maken met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Important]  
> Vanaf versie 1902 biedt Configuration Manager geen ondersteuning voor Linux-of UNIX-clients. 
> 
> Overweeg Microsoft Azure beheer voor het beheer van Linux-servers. Azure-oplossingen hebben uitgebreide Linux-ondersteuning die in de meeste gevallen de functionaliteit van Configuration Manager overschrijden, waaronder end-to-end patch management voor Linux.

Houd rekening met de volgende overwegingen wanneer u toepassingen maakt en implementeert voor computers die Linux en UNIX uitvoeren.  

## <a name="general-considerations"></a>Algemene overwegingen  
 De Configuration Manager-client voor Linux en UNIX biedt ondersteuning voor **Software-implementaties die gebruikmaken van pakketten en Program ma's**. U kunt geen Configuration Manager-toepassingen implementeren op computers met Linux en UNIX.  

 De mogelijkheden van de Linux-en UNIX-software-implementatie zijn:  

-   Software-installatie voor Linux-en UNIX-servers, met inbegrip van de volgende mogelijkheden:  

    -   Nieuwe software-implementatie  

    -   Software-updates voor Program ma's die zich al op een computer bevinden  

    -   BESTURINGSSYSTEEM patches  

-   Systeem eigen Linux-en UNIX-opdrachten en scripts die zich bevinden op Linux-en UNIX-servers  

-   Implementaties die beperkt zijn tot de besturings systemen die u opgeeft wanneer u de programma optie **alleen op opgegeven client platformen** selecteert

-   Onderhouds Vensters om te controleren wanneer software wordt geïnstalleerd

-   Implementatie status berichten voor het bewaken van implementaties  

-   De optie voor de client om netwerk gebruik te beperken bij het downloaden van software van een distributie punt  

### <a name="differences-between-deploying-to-linux-and-unix-computers-and-deploying-to-windows-devices"></a>Verschillen tussen het implementeren van Linux-en UNIX-computers en het implementeren van Windows-apparaten
De belangrijkste verschillen tussen het implementeren van pakketten en Program ma's op Linux-en UNIX-computers en het implementeren van pakketten en Program ma's op Windows-apparaten zijn als volgt:  

|Configuratie|Details|  
|-------------------|-------------|  
|Alleen configuraties gebruiken die bedoeld zijn voor computers en geen configuraties gebruiken die bedoeld zijn voor gebruikers.|De Configuration Manager-client voor Linux en UNIX ondersteunt geen configuraties die bedoeld zijn voor gebruikers.|  
|Configureer Program ma's om software te downloaden van het distributie punt en voer de Program ma's uit vanuit de lokale client cache.|De Configuration Manager-client voor Linux en UNIX biedt geen ondersteuning voor het uitvoeren van software vanaf het distributie punt. In plaats daarvan moet u de software configureren om te downloaden naar de-client en vervolgens installeren.<br /><br /> Nadat de client voor Linux en UNIX software heeft geïnstalleerd, wordt deze software standaard verwijderd uit de cache van de client. Pakketten die zijn geconfigureerd met **persistente inhoud in de client cache** worden echter niet verwijderd van de client en blijven aanwezig in de cache van de client nadat de software is geïnstalleerd.<br /><br /> De client voor Linux en UNIX ondersteunt geen configuraties voor de client cache en de maximale grootte van de client cache wordt alleen beperkt door de vrije schijf ruimte op de client computer.|  
|Het netwerktoegangsaccount voor distributiepunttoegang configureren|Linux-en UNIX-computers zijn ontworpen als werkgroepcomputers. Om toegang te krijgen tot pakketten van het distributie punt in het Configuration Manager site Server domein, moet u het netwerk toegangs account voor de site configureren. U moet dit account opgeven als een componenteigenschap voor softwaredistributie en het account configureren voordat u software implementeert.<br /><br /> U kunt op elke site meerdere netwerktoegangsaccounts configureren. De client voor Linux en UNIX kan elk van de accounts die u configureert als een netwerktoegangsaccount gebruiken.<br /><br /> Zie [site onderdelen voor Configuration Manager](../../core/servers/deploy/configure/site-components.md)voor meer informatie.|  

 U kunt pakketten en programma's implementeren naar verzamelingen die enkel Linux- of UNIX-clients bevatten of u kunt deze implementeren naar verzamelingen met een mengeling van clienttypen, zoals de **Verzameling Alle systemen**. Niet-Linux-en niet-UNIX-clients installeren echter niet de software of het rapport mislukt.  

 Wanneer de Configuration Manager-client voor Linux en UNIX een implementatie ontvangt en uitvoert, worden status berichten gegenereerd. U kunt deze status berichten weer geven in de Configuration Manager-console of door rapporten te gebruiken om de implementatie status te controleren.  

 Zie [pakketten en Program ma's](../../apps/deploy-use/packages-and-programs.md)voor meer informatie over het gebruik van pakketten en Program ma's.  

##  <a name="configure-packages-programs-and-deployments-for-linux-and-unix-servers"></a>Pakketten, Program ma's en implementaties voor Linux-en UNIX-servers configureren  
 U kunt pakketten en Program ma's maken en implementeren met behulp van de beschik bare standaard opties in de Configuration Manager-console. De client vereist geen unieke configuraties.  

 Gebruik de informatie in de volgende secties om pakketten en Program ma's en implementaties te configureren.  

### <a name="packages-and-programs"></a>Pakketten en programma's  
 Als u een pakket en programma voor een Linux-of UNIX-server wilt maken, gebruikt u de **wizard pakket en programma maken** vanuit de Configuration Manager-console. De meest pakketten en programma-instellingen worden door de client voor Linux en UNIX ondersteund. Diverse instellingen worden echter niet ondersteund. Wanneer u een pakket en programma maakt of configureert, moet u rekening houden met de volgende punten:  

-   De bestands typen bevatten die worden ondersteund door de doel computers.  

-   Definieer de opdracht regels die geschikt zijn voor gebruik op de doel computer.  

-   Houd er wel bij dat instellingen die communiceren met gebruikers niet worden ondersteund.  

De volgende tabel geeft een lijst van de eigenschappen voor pakketten en Program ma's die niet worden ondersteund:  

|Pakket- en programma-eigenschap|Gedrag|Meer informatie|  
|----------------------------------|--------------|----------------------|  
|Instellingen van pakketshare:<br /><br /> -Alle opties|Er wordt een fout gegenereerd en de software-installatie mislukt|De client biedt geen ondersteuning voor deze configuratie. De client moet in plaats hiervan de software downloaden met behulp van HTTP of HTTPS en vervolgens de opdrachtregel vanuit de lokale cache uitvoeren.|  
|Instellingen van pakketupdate:<br /><br /> -Gebruikers van distributie punten verbreken|Instellingen worden genegeerd|De client biedt geen ondersteuning voor deze configuratie.|  
|Implementatie-instellingen van besturingssysteem:<br /><br /> -Alle opties|Instellingen worden genegeerd|De client biedt geen ondersteuning voor deze configuratie.|  
|Rapportage:<br /><br /> -Pakket eigenschappen gebruiken voor Status-MIF-koppeling<br /><br /> -Gebruik deze velden voor Status-MIF-koppeling|Instellingen worden genegeerd|De client biedt geen ondersteuning voor het gebruik van Status-MIF-bestanden.|  
|**Uitvoeren**:<br /><br /> -Alle opties|Instellingen worden genegeerd|De client voert altijd pakketten uit zonder gebruikersinterface.<br /><br /> De client negeert alle configuratie-opties voor het uitvoeren.|  
|Na het uitvoeren:<br /><br />-Configuration Manager computer opnieuw opstarten<br /><br /> -Opnieuw opstarten programma besturings elementen<br /><br /> -Configuration Manager de gebruiker afmelden|Er wordt een fout gegenereerd en de software-installatie mislukt|De instelling voor het opnieuw opstarten van het systeem en gebruikersspecifieke instellingen worden niet ondersteund.<br /><br /> Als een andere instelling dan de instelling **Geen actie vereist** in gebruik is, wordt er door de client een fout gegeneerd en wordt de software-installatie voortgezet, maar geen actie ondernomen.|  
|Het programma kan worden uitgevoerd:<br /><br /> -Alleen wanneer een gebruiker is aangemeld|Er wordt een fout gegenereerd en de software-installatie mislukt|Gebruikersspecifieke instellingen worden niet ondersteund.<br /><br /> Als deze optie geconfigureerd is, wordt er door de client een fout gegeneerd en mislukt de software-installatie.<br /><br /> Andere opties worden genegeerd en de software-installatie wordt voortgezet.|  
|Uitvoermodus:<br /><br /> -Uitvoeren met gebruikers rechten|Instellingen worden genegeerd|Gebruikersspecifieke instellingen worden niet ondersteund.<br /><br /> De-client ondersteunt echter de configuratie die wordt uitgevoerd met beheerders rechten.<br /><br /> Wanneer u **uitvoeren met beheerders rechten**opgeeft, gebruikt de Configuration Manager-client de hoofd referenties.<br /><br /> Deze instelling genereert geen fout of logboek vermelding. In plaats daarvan mislukt de installatie van de software wanneer de client een fout genereert voor de vereiste configuratie van het **programma kan** = **alleen worden uitgevoerd wanneer een gebruiker is aangemeld**.|  
|Gebruikers toestaan de programma-installatie te bekijken en ermee te werken|Instellingen worden genegeerd|Gebruikersspecifieke instellingen worden niet ondersteund.<br /><br /> Deze configuratie wordt genegeerd en de software-installatie wordt voortgezet.|  
|Stationsmodus:<br /><br /> -Alle opties|Instellingen worden genegeerd|Deze instelling wordt niet ondersteund omdat inhoud altijd wordt gedownload naar de client en lokaal wordt uitgevoerd.|  
|Eerst een ander programma uitvoeren|Er wordt een fout gegenereerd en de software-installatie mislukt|Recursieve programma-installatie wordt niet ondersteund.<br /><br /> Wanneer een programma is geconfigureerd om eerst een ander programma uit te voeren, mislukt de software-installatie en wordt de andere programma-installatie niet gestart.|  
|Wanneer dit programma wordt toegewezen aan een computer:<br /><br /> -Eenmaal uitvoeren voor elke gebruiker die zich aanmeldt|Instellingen worden genegeerd|Gebruikersspecifieke instellingen worden niet ondersteund.<br /><br /> De client ondersteunt echter de configuratie die wordt uitgevoerd voor de computer.<br /><br /> Deze instelling genereert geen fout of logboek vermelding omdat er al een fout-en logboek vermelding is gemaakt voor de vereiste configuratie van het **programma kan** = **alleen worden uitgevoerd wanneer een gebruiker is aangemeld**.|  
|Programma meldingen onderdrukken|Instellingen worden genegeerd|De client implementeert geen gebruikers interface.<br /><br /> Als deze configuratie is geselecteerd, wordt deze genegeerd en wordt de software-installatie voortgezet.|  
|Dit programma uitschakelen op computers waarop het is geïmplementeerd|Instellingen worden genegeerd|Deze instelling wordt niet ondersteund en heeft geen invloed op de software-installatie.|  
|Toestaan dat dit programma wordt geïnstalleerd vanuit de taken reeks pakket installeren zonder te worden geïmplementeerd||De client biedt geen ondersteuning voor taken reeksen.<br /><br /> Deze instelling wordt niet ondersteund en heeft geen invloed op de software-installatie.|  
|Windows Installer:<br /><br /> -Alle opties|Instellingen worden genegeerd|De client biedt geen ondersteuning voor Windows Installer bestanden of instellingen.|  
|Onderhoudsmodus OpsMgr:<br /><br /> -Alle opties|Instellingen worden genegeerd|De client biedt geen ondersteuning voor deze configuratie.|  

### <a name="deploy-software-to-a-linux-or-unix-server"></a>Software implementeren op een Linux-of UNIX-server
 Als u software wilt implementeren op een Linux-of UNIX-server met behulp van een pakket en programma, kunt u de **wizard software implementeren** gebruiken vanuit de Configuration Manager-console. De meeste implementatie-instellingen worden ondersteund door de client voor Linux en UNIX. Verschillende instellingen worden echter niet ondersteund. Wanneer u software implementeert, moet u rekening houden met de volgende punten:  

- Richt het pakket in op ten minste één distributie punt dat is gekoppeld aan een grens groep die is geconfigureerd voor de locatie van inhoud.  

- De-client voor Linux en UNIX die deze implementatie ontvangt, moet toegang hebben tot dit distributie punt vanaf de netwerk locatie.  

- De client voor Linux en UNIX downloadt het pakket van het distributiepunt en voert het programma uit op de lokale computer.  

- De-client voor Linux en UNIX kan geen pakketten downloaden van gedeelde mappen. Hiermee worden pakketten gedownload van distributie punten met IIS-functionaliteit die HTTP of HTTPS ondersteunen.  

  De volgende tabel bevat de eigenschappen voor implementaties die niet worden ondersteund:  

|Implementatie-eigenschap|Gedrag|Meer informatie|  
|-------------------------|--------------|----------------------|  
|Implementatie-instellingen – doel:<br /><br /> -Beschikbaar<br /><br /> -Vereist|Instellingen worden genegeerd|Gebruikersspecifieke instellingen worden niet ondersteund.<br /><br /> De-client ondersteunt echter de instelling **vereist**, waarmee de geplande installatie tijd wordt afgedwongen, maar de hand matige installatie van vóór die geplande tijd niet wordt ondersteund.|  
|Ontwaakpakketten verzenden|Instellingen worden genegeerd|De client biedt geen ondersteuning voor deze configuratie.|  
|Toewijzingsplanning:<br /><br /> -aanmelden<br /><br /> -afmelden|Er wordt een fout gegenereerd en de software-installatie mislukt|Gebruikersspecifieke instellingen worden niet ondersteund.<br /><br /> De instelling **Zo snel mogelijk**wordt niettemin door de client ondersteund.|  
|Instellingen voor meldingen:<br /><br /> -Gebruikers toestaan het programma onafhankelijk van toewijzingen uit te voeren|Instellingen worden genegeerd|De client implementeert geen gebruikers interface.|  
|Als de geplande toegewezen tijd bereikt wordt, toestaan dat de volgende activiteiten worden uitgevoerd buiten het onderhoudsvenster:<br /><br /> -Systeem opnieuw opstarten (indien nodig om de installatie te volt ooien)|Er wordt een fout gegenereerd|De client biedt geen ondersteuning voor het opnieuw opstarten van het systeem.|  
|Implementatieoptie voor netwerken voor snelle (LAN-) netwerken:<br /><br /> -Programma uitvoeren vanaf distributie punt|Er wordt een fout gegenereerd en de software-installatie mislukt|De client kan geen software uitvoeren vanaf het distributie punt en in plaats daarvan moet het programma worden gedownload voordat het kan worden uitgevoerd.|  
|Implementatieoptie voor een langzame of onbetrouwbare netwerkgrens of een terugvalbronlocatie voor inhoud:<br /><br /> -Clients toestaan inhoud te delen met andere clients in hetzelfde subnet|Instellingen worden genegeerd|De client biedt geen ondersteuning voor het delen van inhoud tussen peers.|  

 Zie [inhoud en infra structuur voor inhoud beheren voor Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)voor meer informatie over de locatie van de inhoud.  

 Zie [toepassingen implementeren](../../apps/deploy-use/deploy-applications.md)voor meer informatie over het maken van een implementatie.  

##  <a name="manage-network-bandwidth-for-software-downloads-from-distribution-points"></a> Netwerkbandbreedte beheren voor softwaredownloads van distributiepunten  
 De Linux-en UNIX-client ondersteunt besturings elementen voor netwerk bandbreedte wanneer de software van een distributie punt wordt gedownload.  

 De client gebruikt de instellingen voor Background Intelligent overzet (BITS) die u configureert als client instellingen in Configuration Manager, maar implementeert geen BITS. De client controleert in de plaats daarvoor de HTTP-aanvraag chunkgrootte en de inter-chunk vertraging voor de softwaredownload om het gebruik van de netwerkbandbreedte te bewerken.  

 U kunt de clientinstellingen voor **Background Intelligent Transfer** configureren en vervolgens de instellingen op de clientcomputer toepassen om een client te configureren om netwerkbandbreedteregelingen te gebruiken. Als u bandbreedte besturings elementen wilt gebruiken, moet de client client instellingen ontvangen voor **Background Intelligent overboeking** met de volgende instellingen die zijn geconfigureerd als **Ja**:  

- **Beperk de maximale netwerkbandbreedte voor BITS-overdrachten op de achtergrond**  

  De volgende configuraties voor de Background Intelligent Transfer worden door de client ondersteund:  

  -   **Begintijd beperkingsvenster**  

  -   **Eindtijd beperkingsvenster**  

  -   **Maximale overdrachtssnelheid tijdens het beperkingsvenster (Kbps)**  

  -   **Maximale overdrachtssnelheid buiten het beperkingsvenster (Kbps)**  

De volgende configuratie voor Background Intelligent Transfer wordt niet ondersteund en wordt genegeerd door de client voor Linux en UNIX:  

- **BITS-downloads buiten het beperkingsvenster toestaan**  

  Als het downloaden van software naar de client vanaf een distributie punt wordt onderbroken, wordt de down load niet hervat door de client voor Linux en UNIX. In plaats daarvan wordt de down load van het volledige software pakket opnieuw gestart.  

##  <a name="configure-operations-for-software-deployments"></a>Bewerkingen voor software-implementaties configureren  
 Net als bij de Windows-client detecteert de Configuration Manager-client voor Linux en UNIX nieuwe software-implementaties tijdens het navragen en controleren op nieuw beleid. De frequentie waarmee de client zoekt naar nieuw beleid is afhankelijk van de clientinstellingen. U kunt onderhoudsvensters configureren om te controleren wanneer software-implementaties plaatsvinden.  

 U kunt software-implementaties configureren naar Linux- en UNIX-servers met behulp van pakketeigenschappen, programma-eigenschappen en implementatie-eigenschappen.  

 Wanneer de clients beleid voor een implementatie ontvangt, wordt een statusbericht verzonden. Er worden ook status berichten verzonden wanneer de installatie van de software wordt gestart en wanneer de installatie wordt voltooid of mislukt.  

 Program ma's voor software-implementaties worden uitgevoerd met de hoofd referenties waarmee de Configuration Manager-client voor Linux en UNIX wordt uitgevoerd. De afsluitcode van de programma-opdracht wordt gebruikt om slagen of mislukken te bepalen. Een afsluitcode 0 (nul) wordt beschouwd als geslaagd. Bovendien worden de **stdout** (standaarduitvoerstroom) en **stderr** (standaardfoutstroom) gekopieerd naar het logbestand wanneer het logboekniveau ingesteld wordt op INFO of TRACE.  

> [!TIP]  
>  Als de software die u wilt implementeren zich bevindt op een Network File System (NFS)-share waartoe de Linux- of UNIX-server toegang heeft, hebt u geen distributiepunt nodig om het pakket te downloaden. Als u in plaats hiervan het pakket maakt, select u het selectievakje voor **Dit pakket bevat bronbestanden**niet. Als u het programma configureert, geeft u de geschikte opdrachtregel op voor rechtstreekse toegang van het pakket tot het NFS-koppelpunt.  
