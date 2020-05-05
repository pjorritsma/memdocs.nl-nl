---
title: Peer-cache van client
titleSuffix: Configuration Manager
description: Gebruik client-peer-cache voor bron locaties bij het implementeren van inhoud met Configuration Manager.
ms.date: 09/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c302e839c2a41ba27d160db24928f7e202de78dc
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110182"
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Peer-cache voor Configuration Manager-clients

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--1101436-->
Peer-cache gebruiken voor het beheren van de implementatie van inhoud naar clients op externe locaties. Peer-cache is een ingebouwde Configuration Manager oplossing waarmee clients rechtstreeks vanuit hun lokale cache inhoud met andere clients kunnen delen.   

> [!Note]  
> In versie 1906 Configuration Manager deze functie standaard ingeschakeld. In versie 1902 of eerder is Configuration Manager deze optionele functie standaard niet ingeschakeld. U moet deze functie inschakelen voordat u deze kunt gebruiken. Zie voor meer informatie [Enable optional features from updates](../../servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  



## <a name="overview"></a>Overzicht

Definities  

- **Peer-cache-client**: elke Configuration Manager-client die inhoud van een peer downloadt  

- **Peer-cache-bron**: een Configuration Manager-client die u inschakelt voor peer-cache en die inhoud heeft om te delen met andere clients  

Gebruik client instellingen om clients peer-cache bronnen te maken. U hoeft peer-cache-clients niet in te scha kelen. Wanneer u clients als peer-cache bronnen wilt inschakelen, bevat het beheer punt deze in de lijst met locatie bronnen voor inhoud.<!--510397--> Zie [bewerkingen](#operations)voor meer informatie over dit proces.  

Een peer-cache bron moet lid zijn van de huidige grens groep van de peer-cache client. Het beheer punt bevat geen peer-cache bronnen van een grens groep in de lijst met inhouds bronnen die de client levert. Het bevat alleen distributie punten van een grens groep in de nabijheid. Zie [grens groepen](../../servers/deploy/configure/boundary-groups.md)voor meer informatie over de grenzen van huidige en grens groepen.<!--SCCMDocs issue 685-->  

De Configuration Manager-client gebruikt peer-cache voor andere clients elk type inhoud in de cache. Deze inhoud bevat Microsoft 365-apps voor Enter prise-bestanden en bestanden voor snelle installatie.<!--SMS.500850-->  

Peer-cache vervangt niet het gebruik van andere oplossingen, zoals Windows BranchCache of leverings optimalisatie. Peer-cache werkt samen met andere oplossingen. Deze technologieën bieden u meer opties voor het uitbreiden van traditionele oplossingen voor inhouds implementatie, zoals distributie punten. Peer-cache is een aangepaste oplossing zonder afhankelijkheid van BranchCache. Als u BranchCache niet inschakelt of gebruikt, werkt peer-cache nog steeds.  

> [!Note]  
> Vanaf versie 1802 is Windows BranchCache altijd ingeschakeld voor implementaties. De instelling waarmee **clients inhoud kunnen delen met andere clients in hetzelfde subnet** , wordt verwijderd.<!--SCCMDocs issue 539--> Als het distributie punt dit ondersteunt en is ingeschakeld in de client instellingen, gebruiken clients BranchCache. Zie [BranchCache configureren](../../clients/deploy/about-client-settings.md#configure-branchcache)voor meer informatie.<!--SCCMDocs issue 735-->   



## <a name="operations"></a>Bewerkingen

Implementeer de [client instellingen](#bkmk_settings) voor een verzameling om peer-cache in te scha kelen. Vervolgens fungeren leden van die verzameling als peer-cache bron voor andere clients in dezelfde grens groep.  

- Een client die fungeert als een peer-inhouds bron, verzendt een lijst met beschik bare inhoud in de cache naar het beheer punt met behulp van status berichten.

   > [!NOTE]
   > Zie [status berichten in Configuration Manager](state-messaging-system-center-configuration-manager.md#7200-state_topictype_super_peer_update_cache_map) voor de lijst met toepasselijke peer-inhouds bron status berichten specifcally die met de status bericht-id's 7200, 7201, 7202 en 7203.

- Een andere client in dezelfde grens groep maakt een inhouds locatie aanvraag naar het beheer punt. De server retourneert de lijst met mogelijke inhouds bronnen. Deze lijst bevat elke peer-cache bron met de inhoud en is online. Het bevat ook de distributie punten en andere inhouds bron locaties in die grens groep. Zie [prioriteit van inhouds bron](fundamental-concepts-for-content-management.md#content-source-priority)voor meer informatie.  

- Op de gebruikelijke manier selecteert de client die de inhoud aanvraagt één bron in de lijst. De client probeert vervolgens de inhoud op te halen.  

Vanaf versie 1806 bevatten grens groepen extra instellingen om u meer controle te geven over de distributie van inhoud in uw omgeving. Zie voor meer informatie [Opties voor grens groepen voor het downloaden van peers](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).<!--1356193-->

> [!NOTE]  
> Als de client terugvalt op een grens groep in de nabijheid voor inhoud, voegt het beheer punt de peer-cache bronnen niet toe van de grens groep van de neighbor aan de lijst met potentiële inhouds bron locaties.  

Kies alleen clients die het meest geschikt zijn als peer-cache bronnen. Evalueer client geschiktheid op basis van kenmerken zoals chassis type, schijf ruimte en netwerk verbinding. Zie [deze blog van een micro soft-consultant](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/configuration-manager-peer-cache-custom-reporting-examples/ba-p/570801)voor meer informatie over het selecteren van de beste clients die moeten worden gebruikt voor peer-cache.


### <a name="limited-access-to-a-peer-cache-source"></a>Beperkte toegang tot de bron van een peer-cache  

Een peer-cache bron weigert aanvragen voor inhoud wanneer aan een van de volgende voor waarden wordt voldaan op het moment dat een peer inhoud vraagt:  

- Modus voor laag accu niveau  

- Processor belasting overschrijdt 80%  

- Schijf-I/O heeft een *AvgDiskQueueLength* die groter is dan 10  

- Er zijn geen meer beschik bare verbindingen met de computer  

> [!Tip]  
> Configureer deze instellingen met de WMI-klasse van de client configuratie server voor de functie peer source (*SMS_WinPEPeerCacheConfig*) in de Configuration Manager SDK.  

Wanneer de peer-cache bron een aanvraag voor de inhoud afwijst, blijft de peer-cache-client inhoud zoeken in de lijst met inhouds bron locaties.   



## <a name="requirements"></a>Vereisten

- Peer-cache ondersteunt alle Windows-versies die worden weer gegeven als ondersteund in [ondersteunde besturings systemen voor clients en apparaten](../configs/supported-operating-systems-for-clients-and-devices.md). Niet-Windows-besturings systemen worden niet ondersteund als peer-cache bronnen of peer-cache-clients.  

- Een peer-cache bron moet een Configuration Manager client zijn die lid is van een domein. Een client die niet lid is van een domein, kan echter wel inhoud ophalen van een aan een domein gekoppelde peer-cache bron.  

- Clients kunnen alleen inhoud downloaden van peer-cache bronnen in hun huidige grens groep.  

- Een [netwerk toegangs account](accounts.md#network-access-account) is niet vereist met de volgende uitzonde ring:  

  - Configureer een netwerk toegangs account in de site wanneer een client met peer-caching een taken reeks uitvoert vanuit software Center en opnieuw opstart naar een opstart installatie kopie. Wanneer het apparaat zich in Windows PE bevindt, wordt het netwerk toegangs account gebruikt voor het ophalen van inhoud van de peer-cache bron.  

  - Als dat nodig is, gebruikt de peer-cache bron het netwerk toegangs account voor het verifiëren van download aanvragen van peers. Voor dit account zijn alleen domein gebruikers machtigingen vereist voor dit doel.  

- Met versie 1802 en eerder bepaalt de laatste aanvraag voor heartbeat-detectie van de client de huidige grens van een peer-cache bron. Een client die wordt geroamd naar een andere grens groep, kan nog steeds lid zijn van de voormalige grens groep voor de doel einden van de peer-cache. Dit gedrag leidt ertoe dat een client een peer-cache bron aangeboden die zich niet op de onmiddellijke netwerk locatie bevindt. Schakel zwervende clients niet in als peer-cache bron.<!--SCCMDocs issue 641-->  

  > [!Important]  
  > Vanaf versie 1806 is Configuration Manager efficiënter bij het bepalen of een peer-cache bron is geroamd naar een andere locatie. Dit gedrag zorgt ervoor dat het beheer punt dit als een inhouds bron levert aan clients op de nieuwe locatie en niet op de oude locatie. Als u de functie voor peer-cache gebruikt met zwervende peer-cache bronnen, moet u na het bijwerken van de site naar versie 1806 ook alle peer-cache bronnen bijwerken naar de meest recente client versie. Het beheer punt bevat deze peer-cache bronnen niet in de lijst met inhouds locaties totdat ze zijn bijgewerkt naar ten minste versie 1806.<!--SCCMDocs issue 850-->  

- Voordat u probeert inhoud te downloaden, valideert het beheer punt eerst of de bron van de peer-cache online is.<!--sms.498675--> Deze validatie vindt plaats via de ' Fast Channel ' voor client meldingen, die TCP-poort 10123 gebruikt.<!--511673-->  

> [!Note]  
> Als u gebruik wilt maken van nieuwe Configuration Manager functies, moet u clients eerst bijwerken naar de nieuwste versie. Wanneer u de-site en-console bijwerkt terwijl er nieuwe functionaliteit wordt weer gegeven in de Configuration Manager-console, is het volledige scenario niet functioneel totdat de client versie ook het meest recent is.  



## <a name="peer-cache-client-settings"></a><a name="bkmk_settings"></a>Client instellingen voor peer-cache

Zie [client cache-instellingen](../../clients/deploy/about-client-settings.md#client-cache-settings)voor meer informatie over de client instellingen voor peer-caching. 

Zie [client instellingen configureren](../../clients/deploy/configure-client-settings.md)voor meer informatie over het configureren van deze instellingen.

Op peer-caching-clients die gebruikmaken van de Windows Firewall, Configuration Manager de firewall poorten configureren die u opgeeft in client instellingen.



## <a name="partial-download-support"></a><a name="bkmk_parts"></a>Gedeeltelijke download ondersteuning
<!--1357346-->
Vanaf versie 1806 kunnen peer-cache bronnen van de client nu inhoud delen in delen. Deze onderdelen minimaliseren de netwerk overdracht om WAN-gebruik te verminderen. Het beheer punt biedt gedetailleerdere tracking van de inhouds onderdelen. Er wordt geprobeerd om meer dan één down load van dezelfde inhoud per grens groep te verwijderen. 


### <a name="example-scenario"></a>Voorbeeldscenario

Contoso heeft één primaire site met twee grens groepen: hoofd kantoor (hoofd kantoor) en filialen. Er is een terugval relatie van 30 minuten tussen de grens groepen. Het beheer punt en distributie punt voor de site bevinden zich alleen in de hoofd kantoor-grens. De vestiging van het filiaal heeft geen lokaal distributie punt. Twee van de vier clients in het filiaal worden geconfigureerd als peer-cache bronnen. 

![Diagram van de netwerk configuratie zoals beschreven in het voorbeeld scenario](media/1357346-peer-cache-source-parts.png)

1. U richt een implementatie met inhoud op alle vier clients in het filiaal. U distribueert de inhoud alleen naar het distributie punt.  

2. Client3 en Client4 hebben geen lokale bron voor de implementatie. Het beheer punt zorgt ervoor dat clients 30 minuten wachten voordat ze terugvallen op de externe grens groep.  

3. CLIENT1 (PCS1) is de eerste peer-cache bron voor het vernieuwen van het beleid met het beheer punt. Omdat deze client als bron van een peer-cache is ingeschakeld, geeft het beheer punt aan dat het downloaden van onderdeel A onmiddellijk vanaf het distributie punt wordt gestart.  

4. Wanneer CLIENT2 (PCS2) contact opneemt met het beheer punt, wordt door het beheer punt automatisch het downloaden van deel B vanaf het distributie punt in de huidige staat uitgevoerd, maar nog niet voltooid.  

5. PCS1 voltooit deel A en brengt onmiddellijk op de hoogte van het beheer punt. Als deel B wordt al uitgevoerd, maar nog niet is voltooid, geeft het beheer punt aan dat deel C vanaf het distributie punt moet worden gedownload.  

6. PCS2 voltooit deel B en waarschuwt onmiddellijk het beheer punt. Het beheer punt geeft aan dat het downloaden van deel D van het distributie punt begint.  

7. PCS1 voltooit het downloaden van deel C en brengt onmiddellijk op de hoogte van het beheer punt. Het beheer punt informeert dat er geen onderdelen meer beschikbaar zijn vanaf het externe distributie punt. Het beheer punt geeft aan dat deel B kan worden gedownload van de lokale peer, PCS2.  

8. Dit proces wordt voortgezet totdat beide client peer-cache bronnen alle onderdelen van elkaar hebben. Het beheer punt prioriteert onderdelen van het externe distributie punt voordat de peer-cache bronnen worden geïnstrueerd om onderdelen van lokale peers te downloaden.  

9. Client3 is de eerste keer dat u het beleid vernieuwt nadat de terugval periode van 30 minuten is verlopen. Er wordt nu weer gecontroleerd op het beheer punt, waarmee de client van nieuwe lokale bronnen wordt geïnformeerd. In plaats van de inhoud volledig te downloaden van het distributie punt via het WAN, wordt de inhoud volledig gedownload van een van de peer-cache bronnen van de client. Clients geven prioriteit aan lokale peer bronnen. 

> [!Note]  
> Als het aantal cache bronnen van de client peer groter is dan het aantal inhouds onderdelen, geeft het beheer punt de extra peer-cache bronnen de opdracht om te wachten op terugval, zoals een normale client. 


### <a name="configure-partial-download"></a>Gedeeltelijke down load configureren

1. Stel [grens groepen](../../servers/deploy/configure/boundary-groups.md) en peer-cache bronnen per normaal in.  

2. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer **sites**. Klik op **hiërarchie-instellingen** in het lint.  

3. Schakel op het tabblad **Algemeen** de optie voor het **configureren van cache bronnen voor client peer in om inhoud in delen te verdelen**.  

4. Maak een vereiste implementatie met inhoud.  

   > [!Note]  
   > Deze functie werkt alleen wanneer de client inhoud op de achtergrond downloadt, bijvoorbeeld met een vereiste implementatie. Down loads op aanvraag, bijvoorbeeld wanneer de gebruiker een beschik bare implementatie in Software Center installeert, gedraagt zich op de gebruikelijke manier.  

Als u wilt zien hoe het downloaden van inhoud in delen wordt verwerkt, bekijkt u de **ContentTransferManager. log** op de client peer-cache bron en het **MP_Location. log** op het beheer punt.  



## <a name="guidance-for-cache-management"></a>Richt lijnen voor cache beheer
<!--510645-->
Peer-cache is afhankelijk van de Configuration Manager-client cache om inhoud te delen. Houd rekening met de volgende punten voor het beheren van de client cache in uw omgeving:  

- De Configuration Manager-client cache is niet vergelijkbaar met de inhouds bibliotheek op een distributie punt. Tijdens het beheren van de inhoud die u distribueert naar een distributie punt, beheert de Configuration Manager-client automatisch de inhoud in de cache. Er zijn instellingen en methoden waarmee u kunt bepalen welke inhoud zich bevindt in de cache van een peer-cache bron. Zie [de client cache voor Configuration Manager-clients configureren](../../clients/manage/manage-clients.md#BKMK_ClientCache)voor meer informatie.  

- De normale cache grootte en-onderhoud zijn van toepassing op peer-cache bronnen. Zie de [client cache grootte configureren](../../clients/deploy/about-client-settings.md#configure-client-cache-size)voor meer informatie. Houd rekening met de grootte van grotere inhoud, zoals OS-upgrade pakketten of Windows 10 Express update-bestanden. Vergelijk uw behoefte aan deze inhoud met de beschik bare schijf ruimte op peer-cache bronnen.  

- De peer-cache-bron-client werkt de laatst gerefereerde tijd van de inhoud in de cache bij wanneer een peer deze downloadt. De client gebruikt deze tijds tempel wanneer de cache automatisch wordt bewaard en de oude inhoud eerst wordt verwijderd. Daarom moet worden gewacht op het verwijderen van inhoud die peer-cache-clients vaker worden gedownload, als dat zo is.  

- Als dat nodig is, kunt u tijdens een taken reeks voor besturingssysteem implementatie de **SMSTSPreserveContent** -variabele gebruiken om inhoud in de client cache te plaatsen. Zie [taken reeks variabelen](../../../osd/understand/task-sequence-variables.md#SMSTSPreserveContent)voor meer informatie.  

- Als dat nodig is, kunt u bij het maken van de volgende software de optie gebruiken om **inhoud in de cache van de client**op te slaan:  
  - Toepassingen
  - Pakketten
  - Installatiekopieën van het besturingssysteem
  - OS-upgrade pakketten
  - Installatiekopieën



## <a name="monitoring"></a>Bewaking   

Bekijk het dash board **client gegevens bronnen** voor meer informatie over het gebruik van peer-cache. Zie [dash board client gegevens bronnen](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard)voor meer informatie.

Gebruik ook rapporten om het gebruik van de peer-cache weer te geven. Ga in de-console naar de werk ruimte **bewaking** , vouw **rapportage**uit en selecteer het knoop punt **rapporten** . De volgende rapporten hebben allemaal een soort **software distributie-inhoud**:  

1.  **Afwijzing van bron inhoud van peer-cache**: hoe vaak de peer-cache bronnen in een grens groep een inhouds aanvraag afwijzen.  

    > [!Note]  
    > **Bekend probleem**<!--486652-->: Wanneer u inzoomt op resultaten zoals *MaxCPULoad* of *MaxDiskIO*, wordt er mogelijk een fout bericht weer gegeven waarin wordt voorgesteld dat het rapport of de details niet worden gevonden. U kunt dit probleem omzeilen door de andere twee rapporten te gebruiken die de resultaten direct weer geven.  

2. **Afwijzing van bron inhoud peer-cache op voor waarde**: toont details van afwijzingen voor een opgegeven grens groep of afwijzings type. 

    > [!Note]  
    > **Bekend probleem**<!--486652-->: U kunt geen van de beschik bare para meters selecteren en in plaats daarvan moet u ze hand matig invoeren. Voer de waarden in voor de *grens groepsnaam* en het *afwijzings type* zoals wordt weer gegeven in het rapport **afwijzing van de bron inhoud** van de peer-cache. Voor het *type afwijzing* kunt u bijvoorbeeld *MaxCPULoad* of *MaxDiskIO*invoeren.  

3. **Details afwijzing van de bron inhoud**van de peer-cache: de inhoud weer geven die door de client is aangevraagd wanneer deze is geweigerd.  

    > [!Note]  
    > **Bekend probleem**<!--486652-->: U kunt geen van de beschik bare para meters selecteren en in plaats daarvan moet u ze hand matig invoeren. Voer de waarde voor het *afwijzings type* in die wordt weer gegeven in het rapport **afwijzing van de peer-cache bron inhoud** . Voer vervolgens de *resource-id* in voor de inhouds bron waarover u meer informatie wilt. 
    > 
    > De resource-ID van de inhouds bron zoeken:  
    > 
    > 1. Zoek de naam van de computer die wordt weer gegeven als de *peer-cache bron* in de resultaten van het **afkeuren van de bron inhoud van de peer-cache door een voor waarden** rapport.  
    > 
    > 2. Ga naar de werk ruimte **activa en naleving** , selecteer het knoop punt **apparaten** en zoek de naam van de computer. Gebruik de waarde in de kolom Resource-ID.  

