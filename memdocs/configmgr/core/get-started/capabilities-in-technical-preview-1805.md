---
title: Technical Preview 1805
titleSuffix: Configuration Manager
description: Meer informatie over nieuwe functies die beschikbaar zijn in de Configuration Manager Technical Preview versie 1805.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7996b3eb-5259-483b-af40-adae2943d123
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: d8c1cd6610bd09b2714951d8a755770b6347b2f6
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905235"
---
# <a name="capabilities-in-technical-preview-1805-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1805 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1805. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Technical Preview-site. 

Raadpleeg het artikel [Technical Preview](technical-preview.md) voordat u deze update installeert. In dit artikel wordt u vertrouwd met de algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="bkmk_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



</br>

**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  



## <a name="create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence"></a>Een gefaseerde implementatie met hand matig geconfigureerde fasen voor een taken reeks maken
<!--1358148-->
U kunt nu [een gefaseerde implementatie](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) met hand matig geconfigureerde fasen voor een taken reeks maken. U kunt Maxi maal 10 extra fasen toevoegen op het tabblad **fasen** van de wizard gefaseerde implementatie maken. 


### <a name="try-it-out"></a>Probeer het nu!
Volg de instructies voor het maken van een gefaseerde implementatie waarbij u alle fasen hand matig configureert. Verzend [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) zodat we weten hoe dit werkt. 

1. Vouw in de werk ruimte **software bibliotheek** **besturings systemen**uit en selecteer **taken reeksen**.  

2. Klik met de rechter muisknop op een bestaande taken reeks en selecteer **gefaseerde implementatie maken**.  

3. Geef op het tabblad **Algemeen** de gefaseerde implementatie een naam, beschrijving (optioneel) en selecteer **hand matig alle fasen configureren**.  

4. Klik op het tabblad **fasen** op **toevoegen**.  

5. Geef een **naam** op voor de fase en blader vervolgens naar de doel **fase verzameling**.  

6. Kies op het tabblad **fase-instellingen** één optie voor elk van de plannings instellingen en selecteer **volgende** als u klaar bent.  

    - Criteria voor het slagen van de vorige fase (deze optie is uitgeschakeld voor de eerste fase.)
        - **Percentage geslaagde implementaties**: Geef het percentage van de apparaten op waarmee de implementatie van de voor gaande fase slagen is voltooid.  

    - Voor waarden voor het starten van deze implementatie fase na een geslaagde uitvoering van de vorige fase  
        - **Deze fase automatisch starten na een uitstel periode (in dagen)**: Kies het aantal dagen dat moet worden gewacht voordat de volgende fase wordt gestart nadat de vorige fase is voltooid. 
        - **Deze fase van de implementatie hand matig starten**: deze fase wordt niet automatisch gestart na het slagen van de vorige fase.  

    - Nadat een apparaat is gericht, installeert u de software
        - **Zo spoedig mogelijk**: stelt de deadline in voor installatie op het apparaat zodra het apparaat is gericht.
        - **Tijd van de deadline (ten opzichte van de tijd waarop het apparaat is gericht)**: de deadline instellen voor de installatie van een bepaald aantal dagen nadat het apparaat is benaderd.  
     
7. Voltooi de wizard fase-instellingen.

8. Op het tabblad **fasen** van de wizard gefaseerde implementatie kunt u nu de fasen voor deze implementatie toevoegen, verwijderen, opnieuw rangschikken of bewerken.  

9. Voltooi de wizard gefaseerde implementatie maken.  



## <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Ondersteuning voor Cloud distributiepunt voor Azure Resource Manager
<!--1322209-->
Bij het maken van een exemplaar van het [Cloud distributiepunt](../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)biedt de wizard nu de mogelijkheid om een **Azure Resource Manager-implementatie**te maken. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) is een modern platform voor het beheren van alle oplossings resources als één entiteit, een zogenaamde [resource groep](/azure/azure-resource-manager/resource-group-overview#resource-groups). Wanneer u een Cloud distributiepunt implementeert met Azure Resource Manager, gebruikt de site Azure Active Directory (Azure AD) om de benodigde cloud resources te verifiëren en te maken. Voor deze moderne implementatie is het klassieke Azure-beheer certificaat niet vereist.  

De wizard Cloud distributiepunt biedt nog steeds de optie voor een **klassieke service-implementatie** met behulp van een Azure-beheer certificaat. Voor het vereenvoudigen van de implementatie en het beheer van resources, raden we u aan het Azure Resource Manager-implementatie model te gebruiken voor alle nieuwe Cloud distributiepunten. Implementeer, indien mogelijk, bestaande Cloud distributiepunten opnieuw met behulp van Resource Manager.

Configuration Manager migreert geen bestaande klassieke Cloud distributiepunten naar het Azure Resource Manager-implementatie model. Nieuwe Cloud distributiepunten maken met Azure Resource Manager-implementaties en vervolgens klassieke Cloud distributiepunten verwijderen. 

> [!IMPORTANT]  
> Deze functie biedt geen ondersteuning voor Azure Cloud service providers (CSP). De implementatie van het Cloud distributiepunt met Azure Resource Manager blijft de klassieke Cloud service gebruiken, wat niet wordt ondersteund door de CSP. Zie [beschik bare Azure-Services in azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services)voor meer informatie.  


### <a name="prerequisites"></a>Vereisten  
- Integratie met [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md). Azure AD-gebruikers detectie is niet vereist.  

- Dezelfde [vereisten voor een Cloud distributiepunt](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_requirements), met uitzonde ring van het Azure-beheer certificaat.  


### <a name="try-it-out"></a>Probeer het nu!  
 Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

1. Vouw in de Configuration Manager-console de werk ruimte **beheer** **Cloud Services**uit en selecteer vervolgens **Cloud distributiepunten**. Klik op **Cloud distributiepunt maken** op het lint.   

2. Selecteer **Azure Resource Manager implementatie**op de pagina **Algemeen** . Klik op **Aanmelden** om te verifiëren met een Azure-abonnement beheerders account. Met de wizard worden de resterende velden automatisch ingevuld op basis van de Azure AD-abonnements gegevens die zijn opgeslagen tijdens de integratie vereisten. Als u meerdere abonnementen hebt, selecteert u het gewenste abonnement. Klik op **Volgende**.  

3. Geef op de pagina **instellingen** op de gebruikelijke wijze het PKI- **certificaat bestand** van de server op. Dit certificaat definieert de FQDN van de Cloud distributiepunt **service** die wordt gebruikt door Azure. Selecteer de **regio**en selecteer vervolgens een optie voor de resource groep om **nieuwe te maken** of **bestaande te gebruiken**. Voer de naam van de nieuwe resource groep in of selecteer een bestaande resource groep in de vervolg keuzelijst.  

4. Voltooi de wizard.  

> [!NOTE]  
> Voor de geselecteerde Azure AD-server-app wijst Azure de machtiging voor het abonnement op de **mede werker** toe.  

Controleer de voortgang van de service-implementatie met **cloudmgr. log** op het service verbindings punt.



## <a name="take-actions-based-on-management-insights"></a>Acties ondernemen op basis van management Insights
<!--1357930-->
Sommige [beheer inzichten](../servers/manage/management-insights.md) hebben nu de mogelijkheid om een actie uit te voeren. Afhankelijk van de regel, vertoont deze actie een van de volgende gedragingen:  

- Navigeer in de-console automatisch naar het knoop punt waar u verdere actie kunt ondernemen. Als door de Management Insight bijvoorbeeld wordt geadviseerd om een client instelling te wijzigen, gaat u naar het knoop punt client instellingen om actie te ondernemen. U kunt verdere actie ondernemen door de standaard-of een aangepast client instellingen-object te wijzigen.  

- Navigeer naar een gefilterde weer gave op basis van een query. Als u bijvoorbeeld actie onderneemt voor de lege verzamelingen regel, worden alleen deze verzamelingen weer gegeven in de lijst met verzamelingen. Hier kunt u verdere actie ondernemen, zoals het verwijderen van een verzameling of het wijzigen van de lidmaatschaps regels.  

De volgende beheer Insight-regels hebben acties in deze release:
- Beveiliging
    - Niet-ondersteunde client versies voor antimalware
- Software Center
    - De nieuwe versie van software Center gebruiken
- Toepassingen
    - Toepassingen zonder implementaties
- Vereenvoudigd beheer
    - Niet-CB-client versies
- Verzamelingen
    - Lege verzamelingen 
- Cloud Services
    - Clients bijwerken naar de nieuwste versie van Windows 10



## <a name="transition-device-configuration-workload-to-intune-using-co-management"></a>De werk belasting van de apparaatconfiguratie overzetten naar intune met behulp van co-beheer
<!--1357903-->

U kunt de werk belasting van de apparaatconfiguratie nu overzetten van Configuration Manager naar intune nadat co-beheer is ingeschakeld. Door deze workload te verwisselen, kunt u intune gebruiken om MDM-beleid te implementeren, terwijl u Configuration Manager gebruikt voor het implementeren van toepassingen. 

Als u deze werk belasting wilt door lopen, gaat u naar de pagina met eigenschappen voor co-beheer en verplaatst u de schuif regelaar van Configuration Manager naar **pilot** of **alle**. Zie voor meer informatie [co-beheer voor Windows 10-apparaten](../../comanage/overview.md).

> [!Note]  
> Door deze werk belasting te verplaatsen, worden ook de werk belasting van **resources** en **Endpoint Protection** verplaatst, die een subset zijn van de werk belasting van de apparaatconfiguratie.

Wanneer u deze werk belasting overschakelt, kunt u nog steeds instellingen van Configuration Manager implementeren op gezamenlijk beheerde apparaten, zelfs als intune de configuratie-instantie van de apparaat is. Deze uitzonde ring kan worden gebruikt om instellingen te configureren die vereist zijn voor uw organisatie, maar die nog niet beschikbaar zijn in intune. Geef deze uitzonde ring op een Configuration Manager configuratie basislijn op. Schakel de optie voor het **altijd Toep assen van deze basis lijn toe, zelfs voor clients die gezamenlijk worden beheerd** bij het maken van de basis lijn of op het tabblad **Algemeen** van de eigenschappen van een bestaande basis lijn. 



## <a name="enable-distribution-points-to-use-network-congestion-control"></a>Distributie punten inschakelen voor het gebruik van congestie beheer van het netwerk
<!--1358112-->

Windows-lage extra vertraging achtergrond transport (LEDBAT) is een functie van Windows Server voor het beheren van achtergrond netwerk overdrachten. Voor distributie punten die worden uitgevoerd op ondersteunde versies van Windows Server, kunt u een optie inschakelen om netwerk verkeer aan te passen. Clients gebruiken alleen netwerk bandbreedte wanneer dit beschikbaar is. 


### <a name="prerequisites"></a>Vereisten
- Een distributie punt op Windows Server, versie 1709.  

- Er is geen client vereiste.<!--SCCMDocs issue 699-->  


### <a name="try-it-out"></a>Probeer het nu!
 Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Selecteer het knoop punt **distributie punten** . Selecteer het doel distributiepunt en klik op **Eigenschappen** in het lint.  

2. Schakel op het tabblad **Algemeen** de optie in om **de download snelheid aan te passen om de ongebruikte netwerk bandbreedte (Windows LEDBAT) te gebruiken**.  



## <a name="cloud-management-dashboard"></a>Dash board voor Cloud beheer
<!--1358461-->
Het nieuwe **dash board voor Cloud beheer** biedt een gecentraliseerde weer gave voor CMG-gebruik (Cloud Management Gateway). Wanneer de site is opgebruikt met Azure AD, worden ook gegevens over Cloud gebruikers en-apparaten weer gegeven.  

De volgende scherm afbeelding is een deel van het dash board voor Cloud beheer met twee van de beschik bare tegels:  
![Cloud beheer dashboard tegels CMG verkeer en huidige online clients](media/1358461-cmg-dashboard.png)

Deze functie bevat ook de **CMG Connection Analyzer** voor real-time verificatie bij het oplossen van problemen. Het console-hulp programma controleert de huidige status van de service en het communicatie kanaal via het CMG-verbindings punt naar een beheer punt dat CMG-verkeer toestaat.


### <a name="prerequisites"></a>Vereisten
- Een actieve [Cloud beheer gateway](../clients/manage/cmg/plan-cloud-management-gateway.md) die wordt gebruikt door clients op internet.  

- De site is onboarding naar [Azure-Services](../servers/deploy/configure/azure-services-wizard.md) voor Cloud beheer.  


### <a name="try-it-out"></a>Probeer het nu!
Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

#### <a name="cloud-management-dashboard"></a>Dash board voor Cloud beheer

Ga in de Configuration Manager-console naar de werk ruimte **bewaking** . Selecteer het knoop punt voor **Cloud beheer** en Bekijk de dashboard tegels.  

#### <a name="cmg-connection-analyzer"></a>CMG Connection Analyzer

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Vouw **Cloud Services** uit en selecteer **Cloud beheer gateway**.  

2. Selecteer de doel-CMG instantie en selecteer vervolgens **verbindings analyse** in het lint.  

3. Selecteer in het venster CMG Connection Analyzer een van de volgende opties om te verifiëren bij de service:  

     1. **Azure AD-gebruiker**: gebruik deze optie om de communicatie te simuleren op dezelfde manier als een cloud-gebaseerde gebruikers-id die is aangemeld bij een Windows 10-apparaat dat is toegevoegd aan Azure AD. Klik op **Aanmelden** om de referenties voor dit Azure AD-gebruikers account veilig in te voeren.  

     2. **Client certificaat**: gebruik deze optie om communicatie te simuleren op dezelfde manier als een Configuration Manager client met een [certificaat voor client verificatie](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_clientauth).  

4. Klik op **starten** om de analyse te starten. De resultaten worden weer gegeven in het venster analyse. Selecteer een vermelding om meer details te bekijken in het veld Beschrijving.  



## <a name="cmpivot"></a>CMPivot
<!--1358456-->
Configuration Manager heeft altijd een grote centrale opslag van apparaatgegevens verschaft, die klanten gebruiken voor rapportage doeleinden. Deze gegevens zijn echter alleen net zo goed als de laatste keer dat deze zijn verzameld van clients. 

CMPivot is een nieuw hulp programma in de console dat toegang biedt tot de real-time status van apparaten in uw omgeving. Er wordt onmiddellijk een query uitgevoerd op alle apparaten die momenteel zijn verbonden in de doel verzameling en de resultaten worden geretourneerd. U kunt deze gegevens vervolgens filteren en groeperen in het hulp programma. Door real-time gegevens op te geven van online-clients, kunt u sneller zakelijke vragen beantwoorden, problemen oplossen en reageren op beveiligings incidenten.

Een van de vereisten is bijvoorbeeld het bijwerken van het systeem-BIOS bij het [beperken van beveiligings problemen van speculatieve uitvoeringen](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974). U kunt CMPivot gebruiken om snel gegevens over het systeem-BIOS op te vragen en clients te zoeken die niet voldoen aan het beleid. 

In deze scherm afbeelding worden in CMPivot twee afzonderlijke BIOS-versies weer gegeven met het aantal apparaten van elkaar. U kunt deze voorbeeld query gebruiken wanneer u CMPivot uitprobeert:  
`Registry('hklm:\\Hardware\\Description\\System\\BIOS') | where (Property == 'BIOSVersion') | summarize dcount( Device ) by Value`  

![CMPivot-venster met voorbeeld query van BIOSVersion](media/1358456-cmpivot-biosversion.png)

U kunt op het aantal apparaten klikken om in te zoomen op de specifieke apparaten. Bij het weer geven van apparaten in CMPivot, kunt u met de rechter muisknop op een apparaat klikken en de volgende [client meldings acties](../clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode)selecteren:
- Script uitvoeren
- Afstandsbediening
- Resource Verkenner

Wanneer u met de rechter muisknop op een specifiek apparaat klikt, kunt u ook de weer gave van het specifieke apparaat naar een van de volgende kenmerken draaien:
- Auto start-opdrachten
- Geïnstalleerde producten
- Processen
- Services
- Gebruikers
- Actieve verbindingen
- Ontbrekende updates

### <a name="prerequisites"></a>Vereisten
- De doel-clients moeten worden bijgewerkt naar de nieuwste versie.  

- De Configuration Manager-beheerder heeft machtigingen nodig voor het uitvoeren van scripts. Zie [beveiligings rollen voor scripts](../../apps/deploy-use/create-deploy-scripts.md#bkmk_ScriptRoles)voor meer informatie.  

### <a name="try-it-out"></a>Probeer het nu!
Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en selecteer **apparaten verzamelingen**. Selecteer een doel verzameling en klik in het lint op **CMPivot starten** om het hulp programma te starten.  

2. De interface biedt meer informatie over het gebruik van het hulp programma. 
     - U kunt hand matig query reeksen bovenaan invoeren of klikken op de koppelingen in de online documentatie.
     - Klik op een van de **entiteiten** om deze toe te voegen aan de query reeks. 
     - De koppelingen voor **tabel operators**, **aggregatie functies**en **scalaire functies** openen taal referentie documentatie in de webbrowser. CMPivot maakt gebruik van dezelfde query taal als [Azure log Analytics](https://docs.microsoft.com/azure/kusto/query/).



## <a name="improved-secure-client-communications"></a>Verbeterde beveiligde client communicatie
<!--1356889,1358228,1358460-->
Het gebruik van HTTPS-communicatie wordt aanbevolen voor alle Configuration Manager communicatie paden, maar dit kan lastig zijn voor sommige klanten vanwege de overhead van het beheer van PKI-certificaten. De introductie van de integratie van Azure Active Directory (Azure AD) vermindert enkele, maar niet alle certificaat vereisten. 

Deze release bevat verbeteringen in de manier waarop clients communiceren met site systemen. Er zijn twee primaire doelen voor deze verbeteringen:  

- U kunt client communicatie beveiligen zonder dat PKI-Server verificatie certificaten nodig zijn.  

- Clients hebben veilig toegang tot inhoud vanaf distributie punten zonder dat hiervoor een netwerk toegangs account nodig is.  

> [!Note]  
> PKI-certificaten zijn nog steeds een geldige optie voor klanten die deze willen gebruiken.  


### <a name="scenarios"></a><a name="bkmk_token"></a>Denkbaar
De volgende scenario's profiteren van deze verbeteringen:  

#### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_token1"></a>Scenario 1: client naar beheer punt
<!--1356889-->
[Apparaten die zijn toegevoegd aan Azure AD](/azure/active-directory/devices/concept-azure-ad-join) kunnen communiceren via een CMG (Cloud Management Gateway) met een beheer punt dat is geconfigureerd voor http. De site server genereert een certificaat voor het beheer punt zodat het kan communiceren via een beveiligd kanaal.   

> [!Note]  
> Dit gedrag is gewijzigd ten opzichte van Configuration Manager 1802 versie van huidige vertakking, waarvoor een HTTPS-ingeschakeld beheer punt is vereist voor dit scenario. Zie [beheer punt voor HTTPS inschakelen](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps)voor meer informatie.  

#### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_token2"></a>Scenario 2: client naar distributie punt
<!--1358228-->
Een werk groep of Azure AD gekoppelde client kan inhoud downloaden via een beveiligd kanaal van een distributie punt dat is geconfigureerd voor HTTP.   

#### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_token3"></a>Scenario 3 Azure AD-apparaat-id 
<!--1358460-->
Een Azure AD-of [Hybrid Azure AD-apparaat](/azure/active-directory/devices/concept-azure-ad-join-hybrid) zonder een aangemelde Azure AD-gebruiker kan veilig communiceren met de toegewezen site. De identiteit van het apparaat in de Cloud is nu voldoende voor verificatie met de CMG en het beheer punt.  


### <a name="prerequisites"></a>Vereisten  

- Een beheer punt dat is geconfigureerd voor HTTP-client verbindingen. Stel deze optie in op het tabblad **Algemeen** van de eigenschappen van de site systeemrol.  

- Een distributie punt dat is geconfigureerd voor HTTP-client verbindingen. Stel deze optie in op het tabblad **Algemeen** van de eigenschappen van de site systeemrol. Schakel de optie om clients niet in staat te stellen **anoniem verbinding te maken**.  

- Een Cloud beheer gateway.  

- Onboarding van de site naar Azure AD voor Cloud beheer.  

    - Als u al aan deze vereiste voor uw site hebt voldaan, moet u de Azure AD-toepassing bijwerken. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer **Azure Active Directory tenants**. Selecteer de Azure AD-Tenant, selecteer de webtoepassing in het deel venster **toepassingen** en klik vervolgens op **toepassings instelling bijwerken** in het lint.  

- Een client met Windows 10 versie 1803 die is gekoppeld aan Azure AD. (Deze vereiste is technisch alleen voor [scenario 3](#bkmk_token3).) 


### <a name="try-it-out"></a>Probeer het nu!
Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer **sites**. Selecteer de site en klik op **Eigenschappen** in het lint.  

2. Schakel over naar het tabblad **communicatie client computer** . Selecteer de optie voor **https of http** en schakel vervolgens de optie nieuw in om door **Configuration Manager gegenereerde certificaten voor http-site systemen te gebruiken**.  

Zie de eerdere [lijst met scenario's](#bkmk_token) om te valideren.

> [!Tip]
> Wacht in deze versie tot 30 minuten voordat het beheer punt het nieuwe certificaat van de site ontvangt en configureert.

U kunt deze certificaten bekijken in de Configuration Manager-console. Ga naar de werk ruimte **beheer** , vouw **beveiliging**uit en selecteer het knoop punt **certificaten** . Zoek naar het basis certificaat van de **SMS-uitgifte** en de certificaten van de site server functie die zijn uitgegeven door de SMS-uitgevende basis.


### <a name="known-issues"></a>Bekende problemen
- De gebruiker kan in Software Center geen toepassingen weer geven die als beschikbaar zijn gericht.  

- Voor implementatie scenario's voor besturings systemen is nog steeds het netwerk toegangs account vereist.  

- Het snel en herhaaldelijk in-en uitschakelen van de optie voor het **gebruik van door Configuration Manager gegenereerde certificaten voor HTTP-site systemen** kan ertoe leiden dat het certificaat niet goed wordt gebonden aan de site systeem rollen. Er zijn geen certificaten uitgegeven door het certificaat ' SMS verlenen ' gebonden aan een website in Windows Server Internet Information Services (IIS). U kunt dit probleem omzeilen door alle certificaten te verwijderen die zijn uitgegeven door ' SMS issued ' in het **SMS** -certificaat archief in Windows, en vervolgens de smsexec-service opnieuw te starten.



## <a name="improvements-for-enabling-third-party-software-update-support"></a>Verbeteringen voor het inschakelen van ondersteuning voor software-updates van derden
<!--1357605-->
Als gevolg van uw UserVoice-feedback over [ondersteuning voor software-updates van derden](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co), wordt deze release verder herhaald op basis van de integratie met System Center updates Publisher (Scup gemaakt). Met Configuration Manager Technical Preview- [versie 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients) is de mogelijkheid voor het lezen van het certificaat van WSUS voor updates van derden toegevoegd en wordt het certificaat vervolgens op clients geïmplementeerd. Maar u moet nog steeds het SCUP gemaakt-hulp programma gebruiken om het certificaat voor het ondertekenen van software-updates van derden te maken en te beheren.

In deze release kunt u de Configuration Manager-site inschakelen om het certificaat automatisch te configureren. De site communiceert met WSUS om een certificaat voor dit doel te genereren. Configuration Manager gaat vervolgens door met het implementeren van dat certificaat voor clients. Deze herhaling verwijdert de nood zaak om het SCUP gemaakt-hulp programma te gebruiken om het certificaat te maken en te beheren. 

Zie [System Center updates Publisher](../../sum/tools/updates-publisher.md)voor meer informatie over algemeen gebruik van het hulp programma Scup gemaakt.

### <a name="prerequisites"></a>Vereisten
- Inschakelen en implementeren van de client instelling **software-updates** van derden inschakelen in de groep met software- **updates** .
- Als WSUS zich op een afzonderlijke server van het software-update punt bevindt, moet u een van de volgende opties op de externe WSUS-server uitvoeren:
    - De Remote Registry-service in Windows inschakelen  
    of
    - Maak in de register sleutel `HKLM\Software\Microsoft\Update Services\Server\Setup` een nieuwe DWORD met de naam **EnableSelfSignedCertificates** met een waarde van `1` . 

### <a name="try-it-out"></a>Probeer het nu!
Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Vouw **site configuratie** uit en selecteer **sites**. Selecteer de site op het hoogste niveau, klik op **site onderdelen configureren** in het lint en selecteer **Software-update punt**.  

2. Schakel over naar het tabblad **updates** van derden. Selecteer de optie om **software-updates van derden in te scha kelen**en selecteer vervolgens de optie voor **Configuration Manager het certificaat automatisch beheert**.

3. Ga verder met de rest van de normale SCUP gemaakt-werk stroom voor het importeren van een Software-Update catalogus van derden en implementeer de updates op clients.



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Taken reeks voor verbeteringen in Windows 10 in-place upgrade
<!--1358500-->

De standaard taken reeks sjabloon voor Windows 10 in-place upgrade bevat nu een andere nieuwe groep met aanbevolen acties om toe te voegen wanneer het upgrade proces mislukt. Deze acties maken het gemakkelijker om problemen op te lossen.

### <a name="new-groups-under-run-actions-on-failure"></a>Nieuwe groepen onder **acties uitvoeren bij fout**
- **Logboeken verzamelen**: als u logboeken van de client wilt verzamelen, voegt u de stappen in deze groep toe. 
    - Een veelvoorkomende procedure is het kopiëren van de logboek bestanden naar een netwerk share. Gebruik de stap [verbinding maken met](../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) netwerkmap om deze verbinding tot stand te brengen. 
    - Als u de Kopieer bewerking wilt uitvoeren, gebruikt u een aangepast script of hulp programma met de [opdracht regel uitvoeren](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) of [Power shell-script uitvoeren](../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript) .
    - Bestanden die moeten worden verzameld, kunnen de volgende logboeken bevatten:  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  
    - Zie [Windows Setup-logboek bestanden](/windows/deployment/upgrade/log-files)voor meer informatie over Setupact. log en andere Windows Setup logboeken.
    - Zie [Configuration Manager client logboeken](../plan-design/hierarchy/log-files.md#BKMK_ClientLogs) voor meer informatie over Configuration Manager client Logboeken.
    - Zie [ingebouwde variabelen voor taken reeksen](../../osd/understand/task-sequence-variables.md) voor meer informatie over _SMSTSLogPath en andere nuttige variabelen.

- **Diagnostische hulpprogram Ma's uitvoeren**: als u aanvullende diagnostische hulpprogram ma's wilt uitvoeren, moet u de stappen in deze groep toevoegen. Deze hulpprogram ma's moeten worden geautomatiseerd voor het verzamelen van aanvullende informatie van het systeem, zodra dit mogelijk is mislukt.
    - Een dergelijk hulp programma is Windows [SetupDiag](/windows/deployment/upgrade/setupdiag). Het is een zelfstandig diagnostisch hulp programma dat u kunt gebruiken voor het verkrijgen van informatie over waarom een Windows 10-upgrade is mislukt.
         - Maak in Configuration Manager [een pakket](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program) voor het hulp programma.
         - Voeg een stap [opdracht regel uitvoeren](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) toe aan deze groep van uw taken reeks. Gebruik de **pakket** optie om te verwijzen naar het hulp programma. De volgende teken reeks is een voor beeld van een **opdracht regel**:  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`



## <a name="cmtrace-installed-with-client"></a>CMTrace geïnstalleerd met client
<!--1357971-->

Het CMTrace-hulp programma voor logboek weergave wordt nu samen met de Configuration Manager-client automatisch geïnstalleerd. Deze wordt toegevoegd aan de installatiemap van de client. Dit is standaard `%WinDir%\ccm\cmtrace.exe` .

> [!Note]  
> CMTrace wordt *niet* automatisch bij Windows geregistreerd om de bestands extensie. log te openen.



## <a name="improvement-to-the-configuration-manager-console"></a>Verbetering van de Configuration Manager-console
<!--1358202-->
De volgende verbeteringen zijn aangebracht in de Configuration Manager-console:

- Apparaat lijsten onder activa en naleving, apparaten, nu standaard de momenteel aangemelde gebruiker weer geven. Deze waarde is als actueel als de [client status](../clients/manage/monitor-clients.md#bkmk_indStatus). De waarde wordt gewist wanneer de gebruiker zich afmeldt. Als er geen gebruiker is aangemeld, is de waarde leeg. 

### <a name="known-issues"></a>Bekende problemen
De waarde van de gebruiker die momenteel is aangemeld, is leeg in het knoop punt apparaten of bij het weer geven van een apparaten lijst onder het knoop punt apparaats verzamelingen. U kunt dit probleem omzeilen door dit [SQL-script](https://gallery.technet.microsoft.com/ConfigMgr-1805-BgbUpdateLiv-306ff46c)te downloaden. Voer sp_BgbUpdateLiveData. SQL uit op de site database server en start de smsexec-en sms_notification_server-Services op het beheer punt opnieuw.<!--514471-->



## <a name="improvements-to-console-feedback"></a>Verbeteringen in console feedback
<!--1357542-->
Deze release bevat de volgende verbeteringen voor het nieuwe [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) mechanisme in de Configuration Manager-console:  

- In het dialoog venster feedback worden nu de vorige instellingen, zoals de geselecteerde opties en uw e-mail adres, opnieuw toegewezen.  

- Offline feedback wordt nu ondersteund. Sla uw feedback op in de-console en upload deze naar micro soft vanaf een systeem met Internet verbinding. Gebruik het nieuwe Uploader-hulp programma voor offline feedback dat zich bevindt in `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe` . Als u de beschik bare en vereiste opdracht regel opties wilt zien, voert u het hulp programma uit met de `--help` optie. Het verbonden systeem moet toegang hebben tot **petrol.Office.Microsoft.com**.

### <a name="known-issues"></a>Bekende problemen
Wanneer u **een glim lach verzenden** gebruikt of **een frons verzendt** vanaf de-console op een computer met een Internet verbinding, kan het volgende bericht worden weer gegeven: ' fout bij het verzenden van feedback '. Als u op **meer details**klikt, wordt de volgende tekst weer gegeven: `{"Message":""}` . Deze fout wordt veroorzaakt door een bekend probleem met de reactie van het back-end-feedback systeem. U kunt de fout negeren. Micro soft heeft uw feedback nog ontvangen. (Als in de details een ander bericht wordt weer gegeven, gebruikt u de optie offline feedback om uw feedback op een later tijdstip opnieuw te verzenden.)



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Verbeteringen van distributie punten met PXE-functionaliteit
<!--1357580-->

Deze release bevat de volgende extra verbeteringen wanneer u de optie gebruikt om [**een PXE-responder zonder Windows Deployment service in te scha kelen**](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) op een distributie punt:  

- Windows Firewall regels worden automatisch gemaakt op het distributie punt wanneer u deze optie inschakelt  
- Verbeteringen aan logboek registratie van onderdelen



## <a name="improvement-to-hardware-inventory-for-large-integer-values"></a>Verbetering van de hardware-inventaris voor grote waarden met gehele getallen
<!--1357880-->
Hardware-inventarisatie heeft momenteel een limiet voor gehele getallen groter dan 4.294.967.296 (2 ^ 32). Deze limiet kan worden bereikt voor kenmerken zoals de grootte van harde schijven in bytes. Het beheer punt verwerkt geen gehele waarden boven deze limiet, waardoor er geen waarde wordt opgeslagen in de data base. Nu in deze release wordt de limiet verhoogd naar 18446744073709551616 (2 ^ 64). 

Voor een eigenschap met een waarde die niet verandert, zoals de totale schijf grootte, ziet u de waarde na het uitvoeren van de upgrade van de site mogelijk niet onmiddellijk. De meeste hardware-inventarisatie is een Delta-rapport. De client verzendt alleen gewijzigde waarden. U kunt dit probleem omzeilen door een andere eigenschap aan dezelfde klasse toe te voegen. Deze bewerking zorgt ervoor dat de client alle eigenschappen van de gewijzigde klasse bijwerkt. 



## <a name="improvement-to-wsus-maintenance"></a>Verbetering van het onderhoud van WSUS
<!--1357898-->

Met de wizard WSUS opruimen worden updates die zijn verlopen of vervangen volgens de vervangings regels, geweigerd. Deze regels worden gedefinieerd in de eigenschappen van de software-update punt component.

### <a name="try-it-out"></a>Probeer het nu!
Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Vouw **site configuratie** uit en selecteer **sites**. Selecteer de site op het hoogste niveau, klik op **site onderdelen configureren** in het lint en selecteer **Software-update punt**.  

2. Schakel over naar het tabblad **vervangings regels** . Schakel de optie in om de **wizard WSUS Cleanup uit te voeren**. Geef het gewenste vervangings gedrag op.  

3. Controleer het bestand bestand Wsyncmgr. log.



## <a name="improvement-to-support-for-cng-certificates"></a>Verbeterde ondersteuning voor CNG-certificaten
<!--1357314-->
In deze release gebruikt u [CNG-certificaten](../plan-design/network/cng-certificates-overview.md) voor de volgende extra HTTPS-server functies:  
- Certificaat registratiepunt, met inbegrip van de NDES-server met de Configuration Manager-beleids module



## <a name="next-steps"></a>Volgende stappen
Zie [Technical Preview voor Configuration Manager voor](technical-preview.md)meer informatie over het installeren of bijwerken van de technische preview-vertakking.    
