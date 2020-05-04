---
title: Virtuele toepassingen van App-V implementeren
titleSuffix: Configuration Manager
description: Bekijk welke overwegingen u moet meenemen wanneer u virtuele toepassingen maakt en implementeert.
ms.date: 03/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: ddcad9f2-a542-4079-83ca-007d7cb44995
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bea7c2ef5c3d77932fcd91ca8d4d2b8baa62edd2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710473"
---
# <a name="deploy-app-v-virtual-applications-with-configuration-manager"></a>Virtuele toepassingen van app-V implementeren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Wanneer u Configuration Manager gebruikt voor het beheren van virtuele toepassingen, profiteert u van de volgende voor delen:  

-   Eén beheer infrastructuur  

-   Functies voor schaal baarheid, implementatie en inhouds distributie, zoals verzamelingen en affiniteit tussen gebruikers en apparaten  

-   Geavanceerde functies voor toepassings beheer  

-   Implementatie van besturings systemen, software-en hardware-inventaris, software licentie controle en Asset Intelligence om virtuele toepassingen te ondersteunen  

Zie [Application Virtualization](https://technet.microsoft.com/library/cc843848.aspx) in de TechNet-bibliotheek voor meer informatie over het maken en sequentieten van toepassingen met micro soft Application Virtualization (app-V).  

Naast de andere Configuration Manager-vereisten en-procedures voor het maken van een toepassing, moet u rekening houden met de volgende overwegingen wanneer u virtuele toepassingen maakt en implementeert:

-   Als u virtuele toepassingen op computers wilt implementeren, moet de Configuration Manager-client en app-V-client op uw computers zijn geïnstalleerd. Clientapparaten kunnen desktop- en draagbare computers, en VDI-clients (Virtual Desktop Infrastructure) zijn. De Configuration Manager-en app-V-client software werken samen om virtuele toepassings pakketten te leveren, te zoeken en te starten. De Configuration Manager-client beheert de levering van virtuele toepassings pakketten naar de app-V-client. De App-V-client voert de virtuele toepassing op de client uit.  

-   U moet voor het implementeren van een virtuele toepassing eerst de virtuele toepassing maken met App-V Application Virtualization Sequencer. De sequencer controleert het installatie- en configuratieproces voor een toepassing en registreert de informatie die nodig is voor het uitvoeren van de toepassing in een virtuele omgeving. U kunt de sequencer ook gebruiken om in te stellen welke bestanden en configuraties van toepassing zijn op alle gebruikers en welke configuraties gebruikers kunnen aanpassen.  

-   Wanneer u een toepassing sequentieert, moet u het pakket opslaan op een locatie waar Configuration Manager toegang toe heeft. U kunt vervolgens een toepassingsimplementatie maken die deze virtuele toepassing bevat.  

-   Configuration Manager biedt geen ondersteuning voor het gebruik van de gedeelde alleen-lezen cache functie van app-V 4,6.  

-   Configuration Manager ondersteunt de functie Shared Content Store in app-V 5.  

-   Wanneer u een implementatie type maakt voor een virtuele toepassing, maakt Configuration Manager het implementatie type met behulp van de inhoud van het manifest bestand van de toepassing. Dit is een XML-bestand met informatie over de virtuele toepassing. Daarnaast maakt Configuration Manager vereisten voor het implementatie type op basis van de inhoud van het OSD-bestand van app-V dat informatie bevat over de ondersteunde besturings systemen voor de virtuele toepassing.  

-   Voor het implementeren van virtuele toepassingen in Configuration Manager moet op client computers mini maal de app-V 4,6 SP1 of een latere versie van de client zijn geïnstalleerd.  

-   Voordat u virtuele toepassingen kunt implementeren, moet u de app-V-client bijwerken met de hotfix die wordt beschreven in het Knowledge Base-artikel [2645225](https://support.microsoft.com/kb/2645225).  

-   Wanneer u verbindings groepen gebruikt in app-V 5,0, kunnen uw geïmplementeerde virtuele toepassingen hetzelfde bestands systeem en REGI ster delen op client computers. In tegenstelling tot standaard virtuele toepassingen kunnen deze toepassingen gegevens met elkaar delen. Verbindingsgroepen behouden bovendien gebruikersinstellingen voor de toepassingen die ze bevatten. Virtuele app-V-omgevingen in Configuration Manager worden gebruikt voor het instellen van verbindings groepen op client computers. Virtuele omgevingen worden op clientcomputers gemaakt of gewijzigd wanneer de toepassing wordt geïnstalleerd of wanneer clients vervolgens hun geïnstalleerde toepassingen evalueren. U kunt prioriteiten aanbrengen in deze toepassingen, zodat de hoogste prioriteit prevaleert wanneer meerdere toepassingen proberen om het bestandssysteem of een registerwaarde te wijzigen. Zie [virtuele omgevingen van app-V maken](../../apps/deploy-use/create-app-v-virtual-environments.md)voor meer informatie.  

##  <a name="supported-app-v-versions"></a> Ondersteunde App-V-versies  
 Configuration Manager ondersteunt de volgende versies van app-V:  

-   **App-V 4,6**: voor het gebruik van virtuele toepassingen in Configuration Manager moeten op client computers de App-v 4,6 SP1, App-v 4,6 SP2 of app-V 4,6 SP3-client zijn geïnstalleerd.  

     Voordat u virtuele toepassingen kunt implementeren, moet u ook de app-V 4,6 SP1-client bijwerken met de hotfix die wordt beschreven in het Knowledge Base-artikel [2645225](https://go.microsoft.com/fwlink/p/?LinkId=237322).  

-   **App-v 5, App-v 5,0 SP1, App-v 5,0 SP2, App-v 5,0 SP3 en App-v 5,1**: voor app-v 5,0 SP2 moet u [hotfix package 5](https://support.microsoft.com/en-us/kb/2963211) installeren of App-v 5,0 SP3 gebruiken.  
-   **App-V 5,2**: dit is ingebouwd in Windows 10 Education (1607 en hoger), Windows 10 Enter prise (1607 en hoger) en Windows Server 2016.

Zie de volgende onderwerpen voor meer informatie over app-V in Windows 10:

- [Wat is er nieuw in app-V](https://technet.microsoft.com/itpro/windows/manage/appv-about-appv)
- [Aan de slag met app-V voor Windows 10](https://technet.microsoft.com/itpro/windows/manage/appv-getting-started)
- [Upgrade uitvoeren naar app-V voor Windows 10 vanaf een bestaande installatie](https://technet.microsoft.com/itpro/windows/manage/appv-upgrading-to-app-v-for-windows-10-from-an-existing-installation)

##  <a name="steps-to-manage-app-v-virtual-applications"></a>Stappen voor het beheren van virtuele toepassingen van App-V  
 Voer de volgende stappen uit om virtuele toepassingen van app-V te beheren:  

1.   **Sequence**: sequentiëren is het proces van het converteren van een toepassing naar een virtuele toepassing met behulp van de app-V-sequencer.

2.   **Maken**: gebruik de wizard implementatie type maken om de geordende toepassing te importeren in een Configuration Manager implementatie type dat u vervolgens kunt toevoegen aan een toepassing. U kunt ook virtuele omgevingen maken die meerdere virtuele toepassingen toestaan om instellingen te delen.

3.   **Distribueren**: distributie is het proces van het maken van app-V-toepassingen beschikbaar op Configuration Manager distributie punten.

4.   **Implementeren**: implementatie is het proces van het beschikbaar maken van de toepassing op client computers. Dit wordt publicatie en streaming genoemd in een volledige app-V-infra structuur.  

##  <a name="configuration-manager-virtual-application-delivery-methods"></a>Leveringsmethoden van virtuele toepassingen in Configuration Manager  
Configuration Manager ondersteunt twee methoden voor de levering van virtuele toepassingen aan clients: streaming-levering en lokale levering (downloaden en uitvoeren).

Wanneer u beslist welke leverings methode u moet gebruiken, vergelijkt u de minder schijf ruimte die nodig is voor het leveren van streaming tegen de gegarandeerde Beschik baarheid van app-V-toepassingen in lokale levering. Lokale levering vereist meer schijfruimte; deze optie kan echter nuttiger zijn voor streaminglevering om gebruikers vanuit eender welke locatie toegang te laten hebben tot de toepassing.  

###  <a name="streaming-delivery"></a>Levering via streaming
Wanneer u Configuration Manager gebruikt voor het beheren van de app-V-client, ondersteunt het het streamen van virtuele toepassingen via HTTP of HTTPS vanaf een distributie punt. Streaming via HTTP of HTTPS is standaard ingeschakeld en wordt ingesteld in het dialoog venster voor eigenschappen van distributie punten. Wanneer u een virtuele toepassing implementeert op client computers en een gebruiker de virtuele toepassing uitvoert, neemt de Configuration Manager-client contact op met een beheer punt om te bepalen welk distributie punt moet worden gebruikt. Vervolgens wordt de toepassing gestreamd vanaf het distributie punt.  

Gebruik de informatie in deze tabel om u te helpen bepalen of het leveren van streaming de beste leverings methode is:

|Voordelen|Nadelen|  
|----------------|-------------------|  
|Deze methode gebruikt standaard netwerkprotocollen om pakketinhoud te streamen vanaf distributiepunten.<br /><br /> Programmasnelkoppelingen voor virtuele toepassingen activeren een verbinding naar het distributiepunt, zodat de levering van de virtuele toepassing op aanvraag gebeurt.<br /><br /> Deze methode werkt goed voor clients met verbindingen met hoge bandbreedte naar de distributiepunten.<br /><br /> Bijgewerkte virtuele toepassingen die over het hele bedrijf zijn geïmplementeerd, zijn beschikbaar wanneer clients beleid ontvangen dat hen informeert dat de huidige versie wordt vervangen; vervolgens downloaden ze alleen de wijzigingen ten opzichte van de vorige versie.<br /><br /> Toegangsmachtigingen worden gedefinieerd aan het distributiepunt om gebruikers te verhinderen om niet-toegestane toepassingen of pakketten te openen.|Virtuele toepassingen worden niet gestreamd totdat de gebruiker de toepassing voor de eerste keer uitvoert. In dit scenario is het mogelijk dat een gebruiker programmasnelkoppelingen ontvangt voor virtuele toepassingen en vervolgens de verbinding met het netwerk verbreekt voordat de virtuele toepassingen voor de eerste keer zijn uitgevoerd. Als de gebruiker de virtuele toepassing probeert uit te voeren terwijl de client offline is, ziet de gebruiker een fout en kan de gevirtualiseerde toepassing niet worden uitgevoerd omdat er geen Configuration Manager distributie punt beschikbaar is om de toepassing te streamen. De toepassing zal niet beschikbaar zijn totdat de gebruiker opnieuw verbinding maakt met het netwerk en de toepassing uitvoert.<br /><br /> U kunt dit vermijden door de lokale leveringsmethode te gebruiken voor het leveren van virtuele toepassingen aan clients. U kunt ook het clientbeheer op internet voor levering via streaming inschakelen.|  

###  <a name="local-delivery-download-and-execute"></a>Lokale levering (downloaden en uitvoeren)  
Downloaden en uitvoeren is de meest voorkomende benadering bij het gebruik van Configuration Manager, omdat deze aanpak nauw keurig wordt gesimuleerd hoe andere toepassings indelingen worden geleverd met Configuration Manager. Wanneer u de lokale leverings methode gebruikt, downloadt de Configuration Manager-client eerst het volledige virtuele toepassings pakket naar de Configuration Manager-client cache. De Configuration Manager geeft de app-V-client de opdracht om de toepassing vanuit de Configuration Manager cache naar de app-V-cache te streamen. Als u een virtuele toepassing implementeert op client computers en de inhoud ervan zich niet in de app-V-cache bevindt, streamt de app-V-client de inhoud van de toepassing van de Configuration Manager-client cache naar de app-V-cache en voert de toepassing vervolgens uit. Nadat de toepassing is uitgevoerd, kunt u de Configuration Manager-client zo instellen dat alle oudere versies van het pakket worden verwijderd tijdens de volgende verwijderings cyclus of dat ze in Configuration Manager-client cache behouden blijven. Het lokaal persistent maken van inhoud kan gebruikmaken van optimalisatie methoden voor de levering van pakket inhoud, zoals BranchCache en peer cache.

Gebruik de informatie in deze tabel om u te helpen bepalen of lokale levering de beste bezorgings methode is voor u:   

|Voordelen|Nadelen|  
|----------------|-------------------|  
|De standaard distributiepuntfunctie wordt gebruikt om het pakket te downloaden door gebruik te maken van BITS (Background Intelligent Transfer Service).<br /><br /> De inhoud van het virtuele toepassings pakket wordt lokaal aan de client geleverd. Dit betekent dat gebruikers ze kunnen uitvoeren wanneer hun computer niet met het netwerk is verbonden.<br /><br /> Deze methode is geschikt voor trage of onbetrouwbare netwerkverbindingen en voor computers die alleen sporadisch verbinding maken met het netwerk.<br /><br /> Configuration Manager maakt gebruik van RDC (Remote Differential Compression) om alleen de bytes te verzenden binnen de bestanden die zijn gewijzigd wanneer de inhoud van het virtuele toepassings pakket wordt bijgewerkt. De Configuration Manager-client gebruikt RDC om een nieuwe versie van een virtueel toepassings pakket te bouwen op basis van de huidige versie van het pakket en eventuele wijzigingen die naar de client worden verzonden.<br /><br /> Deze methode toepassingstolerantie voor mobiele gebruikers of gebruikers zonder netwerkverbinding. Beheerders kunnen ervoor kiezen het pakket op te slaan in de Configuration Manager-cache na de levering als de virtuele toepassing werd geïmplementeerd met een installatie actie. Het pakket in de Configuration Manager-client cache fungeert als een lokale, betrouw bare streaming-bron voor de app-V-client om het pakket in de cache op te halen.|Schijf ruimte die gelijk is aan Maxi maal twee maal de grootte van het virtuele toepassings pakket is vereist op de client wanneer de virtuele toepassing in de Configuration Manager cache wordt bewaard.|  

###  <a name="deployment-from-an-image"></a>Implementatie vanuit een installatie kopie

U kunt virtuele toepassingen ook vooraf installeren op een computer en vervolgens een installatiekopie maken van die computer voor implementatie naar andere computers. Maar als het virtuele toepassings pakket is gemaakt op een andere site, wordt de binaire delta replicatie niet gebruikt om updates naar de toepassing te downloaden. Deze optie kan nuttig zijn in een Virtual Desktop Infrastructure waarbij u wilt dat toepassingen onmiddellijk beschikbaar zijn in plaats van gedownload te moeten worden nadat de gebruiker zich aanmeldt.    

##  <a name="migrating-from-an-app-v-infrastructure-to-a-configuration-manager-and-app-v-infrastructure"></a> Migreren van een App-V-infrastructuur naar een Configuration Manager- en App-V-infrastructuur  
Gebruik de volgende tabel om u te helpen bij het plannen van een migratie van een bestaande app-V-infra structuur naar Virtual Application Management met Configuration Manager.  

|Stap|Meer informatie|  
|----------|----------------------|  
|Controleer uw huidige virtuele toepassingen en kies de toepassingen die u wilt migreren naar uw Configuration Manager-infra structuur.|Geen aanvullende informatie.|  
|Beoordeel de gebruikers en apparaten waarnaar de virtuele toepassingen zullen worden geïmplementeerd.|Maak Configuration Manager verzamelingen om de gebruikers en apparaten te groeperen waarop u de virtuele toepassingen wilt implementeren. Zie [Inleiding tot verzamelingen](../../core/clients/manage/collections/introduction-to-collections.md).|  
|Migreer app-V 5-verbindings groepen naar Configuration Manager virtuele omgevingen.|Zie de sectie [App-V 5-verbindings groepen migreren naar Configuration Manager virtuele omgevingen](deploying-app-v-virtual-applications.md#migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments) in dit onderwerp.|  
|Onderzoek om erachter te komen of uw virtuele toepassingen bestaan als volledige toepassingen in uw Configuration Manager-infra structuur.|Voor eenvoudiger beheer kunt u de virtuele toepassing toevoegen als een nieuw implementatietype naar de bestaande volledige toepassing. Zie [toepassingen maken](../../apps/deploy-use/create-applications.md).|  
|Maken van toepassingen om uw bestaande App-V-pakketten te vervangen.|Zie [Inleiding tot toepassings beheer](../understand/introduction-to-application-management.md) en het [maken van toepassingen](../../apps/deploy-use/create-applications.md).|  
|Configuration Manager begint met het beheren van virtuele toepassingen op een client na de eerste implementatie van een virtuele toepassing. Daarna moet Configuration Manager alle app-V-toepassingen op de computer beheren.|Geen aanvullende informatie.|  
|Distribueer de inhoud naar de geschikte distributiepunten om lokale levering van toepassingen in te schakelen.|Zie [inhoud en infra structuur voor inhoud beheren](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|Implementeer de toepassing om clients te Configuration Manager.<br /><br /> Als de app-V-toepassing is gemaakt met een eerdere versie van de sequencer die geen manifest-XML-bestand maakt, kunt u deze openen en opslaan in een nieuwere versie van de sequencer om het bestand te maken. Dit bestand is vereist om virtuele toepassingen te implementeren met Configuration Manager.<br /><br /> App-V ondersteunt de virtuele toepassings pakketten die zijn gemaakt met de SoftGrid 4,1 SP1-of 4,2-versies van de sequencer.<br /><br /> Als de toepassingen voorheen lokaal zijn geïnstalleerd, moet u deze verwijderen voordat u een virtuele versie ervan implementeert.|Zie [toepassingen implementeren](../../apps/deploy-use/deploy-applications.md).|  
|Configuration Manager biedt geen ondersteuning meer voor het gebruik van pakketten en Program ma's die virtuele toepassingen bevatten. Wanneer u migreert van Configuration Manager 2007 naar Configuration Manager current branch, worden deze pakketten door Configuration Manager geconverteerd naar toepassingen.<br /><br /> Configuration Manager 2007-advertisements worden geconverteerd naar de volgende implementatie typen:<br /><br /> -App-V-pakketten migreren zonder aankondiging: één implementatie type dat de standaard implementatie type-instellingen gebruikt.<br /><br /> -App-V-pakketten migreren met één aankondiging: één implementatie type dat dezelfde instellingen gebruikt als de <br />                Aankondiging van Configuration Manager 2007.<br /><br /> -App-V-pakketten migreren met meerdere aankondigingen: een implementatie type voor elke <br />                Configuration Manager 2007-advertisement, waarbij de instellingen voor die aankondiging worden gebruikt.|Zie [planning voor de migratie van objecten om de huidige vertakking te Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md).|  

##  <a name="migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments"></a>Migrating App-V 5 connection groups to Configuration Manager virtual environments  
Met virtuele app-V-omgevingen in Configuration Manager kunt u virtuele toepassingen die u hebt geïmplementeerd om hetzelfde bestands systeem en REGI ster te delen op client computers. Dit betekent dat deze toepassingen, in tegenstelling tot virtuele standaardtoepassingen, gegevens met elkaar kunnen delen. Virtuele omgevingen worden op clientcomputers gemaakt of gewijzigd wanneer de toepassing wordt geïnstalleerd of wanneer clients vervolgens hun geïnstalleerde toepassingen evalueren. Virtuele omgevingen zijn vergelijkbaar met verbindings groepen in zelfstandige app-V 5.  

Wanneer u verbindings groepen migreert van zelfstandige app-V 5 naar Configuration Manager virtuele omgevingen, moet u ervoor zorgen dat Configuration Manager de verbindings groepen die al bestaan op client computers correct beheert en dat de gebruikers omgeving binnen die verbindings groepen behouden blijft.  

Om app-V 5-verbindings groepen te converteren naar Configuration Manager virtuele omgevingen:  

1.  Maak Configuration Manager-toepassingen voor alle toepassingen die bestonden in app-V.  

2.  Implementeer de toepassingen naar gebruikers op apparaten met een implementatiedoel van **Vereist**. Implementaties naar gebruikers moeten worden geïmplementeerd voor dezelfde gebruikers die de toepassing hebben gebruikt in app-V. Implementaties naar computers moeten worden geïmplementeerd op dezelfde computers die de toepassing hadden in app-V.  

3.  Nadat de implementatie is voltooid, maakt u virtuele omgevingen die overeenkomen met de verbindings groepen die zijn gepubliceerd in de zelfstandige app-V. De virtuele omgeving moet dezelfde pakketten bevatten (met name implementatie typen van app-V 5) in dezelfde volg orde.  

Zie [virtuele toepassingen van App-v maken](../../apps/deploy-use/create-app-v-virtual-environments.md)voor informatie over het maken van een virtuele App-v-omgeving.  

U kunt ook alle verbindings groepen uit de app-V-client verwijderen voordat u begint met het implementeren van toepassingen met Configuration Manager. Maar alle instellingen die gebruikers in app-V-verbindings groepen mogelijk hebben opgeslagen, gaan verloren.  

##  <a name="dynamic-suite-composition-in-app-v-46"></a>Dynamic Suite Composition in App-V 4.6  
Dynamic Suite-compositie is een functie waarmee u één virtueel toepassings pakket kunt definiëren als een afhankelijkheid van een ander virtueel toepassings pakket. Wanneer de toepassing wordt uitgevoerd, host de App-V-client het primaire pakket en het afhankelijke pakket in dezelfde virtuele omgeving van de toepassing.  

Als u deze functie met Configuration Manager wilt gebruiken, moet u beide pakketten implementeren en registreren bij de app-V-client. Om ervoor te zorgen dat de inhoud van het afhankelijke pakket lokaal op de client computer wordt gehost, stelt u de toepassings implementatie in voor lokale levering (downloaden en uitvoeren).  

Zie de App-V-documentatie voor meer informatie over App-V Dynamic Suite Composition.  

##  <a name="converting-app-v-46-applications-to-app-v-5-applications"></a>Converteren van App-V 4.6-toepassingen naar App-V 5-toepassingen  
De indeling van het toepassingspakket voor App-V 5 is gewijzigd ten opzicht van App-V 4.6. Toepassingen die zijn gesequentieerd met App-V 4.6 worden niet meer ondersteund. Maar app-V 5 heeft een pakket conversie programma dat u kunt gebruiken om toepassingen te converteren. Zie de [App-V 5-documentatie](https://technet.microsoft.com/library/jj713472.aspx)voor meer informatie.  

U kunt met behulp van de volgende stappen App-V 4.6-toepassingen converteren naar App-V 5-toepassingen:  

1.  De app-V 4,6-pakketten in de app-V 5-indeling converteren of opnieuw indelen.  

2.  De App-V-5-client implementeren op computers in uw hiërarchie.  

3.  Maak nieuwe toepassingen die implementatietypen bevatten voor uw App-V 5-toepassingen en maak vervangingsregels om de App-V 4.6-toepassingen te vervangen.  

4.  Maak zo nodig virtuele omgevingen.  

5.  Implementeer de nieuwe App-V-5 toepassingen op computers.  

##  <a name="user-and-deployment-configuration-files"></a> Configuratiebestanden voor gebruikers en implementaties  
Configuratie bestanden voor gebruikers en implementaties bevatten instellingen die bepalen hoe een toepassing zich gedraagt. U kunt deze bestanden gebruiken om toepassings instellingen te wijzigen zonder de toepassing opnieuw in te passen.  

Een typische 5 App-V-toepassing bevat mogelijk de volgende bestanden:  

-   Een toepassings pakket bestand (. appv)  

-   Een gebruikers configuratie bestand  

-   Een configuratie bestand voor implementatie  

Het gebruikers configuratie bestand bevat instellingen die alleen van toepassing zijn op de aangemelde gebruiker. U kunt bijvoorbeeld de configuratie bestanden bewerken om de informatie over de snelkoppeling naar de toepassing die voor gebruikers wordt geïmplementeerd, te wijzigen. U kunt ook een Configuration Manager-toepassing maken met meerdere implementatie typen. Elk implementatie type kan een ander gebruikers configuratie bestand bevatten en regels voor vereisten gebruiken om ervoor te zorgen dat deze voor de relevante gebruikers zijn geïnstalleerd.  

Het configuratie bestand van de implementatie bevat instellingen die van toepassing zijn op de computer, zoals register instellingen. Het bestand kan ook gebruikers instellingen bevatten die worden toegepast op alle gebruikers.  

Als u virtuele toepassingen van app-V 5 wilt implementeren met Configuration Manager, moeten alle drie de bestanden aanwezig zijn in dezelfde map wanneer u het app-V 5-implementatie type maakt. Als er zich meerdere bestanden in de map bevinden, maakt Configuration Manager gebruik van de meest recente.  

Zie de [App-V 5-documentatie](https://technet.microsoft.com/library/jj713466.aspx)voor meer informatie.  

##  <a name="app-v-local-interaction"></a> Lokale interactie in App-V  
In sommige scenario's voor toepassings implementaties worden toepassingen lokaal op client computers geïnstalleerd en worden andere toepassingen geïmplementeerd als virtuele toepassingen op dezelfde client computer. Standaard kunnen lokaal geïnstalleerde toepassingen gevirtualiseerde toepassingen niet zien of er rechtstreeks mee communiceren. Dit is het beoogde gedrag van de toepassings isolatie die app-V biedt. Lokale interactie is een functie van de app-V-client die u voor elke toepassing kunt inschakelen zodat lokaal geïnstalleerde toepassingen die worden uitgevoerd op een client computer, de gevirtualiseerde toepassingen kunnen zien en Hiermee kunnen communiceren. Configuration Manager en app-V bieden volledige ondersteuning voor lokale interactie.  

Zie de app-V-documentatie voor meer informatie over de functie voor lokale interactie van app-V.  

##  <a name="app-v-5-shared-content-store"></a>App-V 5 Shared Content Store  
Configuration Manager ondersteunt de functie app-V 5 Shared Content Store. Zie [Planning for the App-V 5.0 Shared Content Store (SCS)](https://technet.microsoft.com/library/jj713431.aspx)voor meer informatie.  

##  <a name="monitoring-virtual-applications"></a>Virtuele toepassingen controleren  

### <a name="virtual-application-reports"></a>Rapporten van virtuele toepassingen  
U kunt de volgende rapporten gebruiken om app-V in uw Configuration Manager omgeving te bewaken:  

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|Resultaten virtuele omgeving App-V|Geeft informatie weer over een geselecteerde virtuele omgeving met een opgegeven status voor een geselecteerde verzameling (alleen app-V 5).|  
|Resultaten virtuele omgeving App-V voor activa|Geeft informatie weer over een geselecteerde virtuele omgeving voor een opgegeven Asset en implementatie typen voor de geselecteerde virtuele omgeving (alleen app-V 5).|  
|Status virtuele omgeving App-V|Geeft compatibiliteits informatie weer voor een geselecteerde virtuele omgeving voor een geselecteerde verzameling. De kolom **bewaard** in dit rapport geeft de activa weer waarin een eerder ingestelde virtuele omgeving niet meer van toepassing is, maar blijft behouden om gebruikers instellingen te blijven gebruiken in toepassingen die in de virtuele omgeving worden uitgevoerd (alleen app-V 5).|  
|Computers met een specifieke virtuele toepassing|Geeft een samen vatting weer van computers die de opgegeven app-V-snelkoppeling hebben die door de Application Virtualization Management sequencer is gemaakt (alleen app-V 4,6).|  
|Computers met een specifiek virtuele-toepassingspakket|Geeft een lijst weer van computers waarop het opgegeven app-V-toepassings pakket is geïnstalleerd (alleen app-V 4,6).|  
|Alle exemplaren van virtuele-toepassingspakketten tellen|Geeft een telling weer van alle gedetecteerde app-V-toepassings pakketten (alleen app-V 4,6).|  
|Alle exemplaren van virtuele toepassingen tellen|Geeft een telling weer van alle gedetecteerde app-V-toepassingen (alleen app-V 4,6).|  

### <a name="log-files"></a>Logboekbestanden  
Configuration Manager registreert informatie over implementaties van virtuele toepassingen in logboek bestanden. Zie [logboek bestanden](../../core/plan-design/hierarchy/log-files.md)voor meer informatie over de logboek bestanden die door virtuele toepassingen en Configuration Manager toepassings beheer worden gebruikt.  

Voor Windows 8,1 zoekt u naar Logboeken voor de app-V-client in C:\ProgramData\Microsoft\Application Virtualization client.  
