---
title: Mogelijkheden van Technical Preview 1606
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview voor Configuration Manager, versie 1606.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 134a2f60-811e-4dc9-a8f5-1ce0018c5c12
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 0513c1908b1360a50653931dda57e5d148055240
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905676"
---
# <a name="capabilities-in-technical-preview-1606-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1606 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1606. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site.      Voordat u deze versie van de Technical Preview installeert, raadpleegt u het inleidende onderwerp, [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md), om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.    

**Bekende problemen in deze technische preview:**  
*  Wanneer u bijwerkt van Technical Preview 1604 naar 1605 en vervolgens naar versie 1606, kan de update mislukken en wordt er een fout weer gegeven die vergelijkbaar is met het volgende, wordt vastgelegd in **cmupdate. log**:

    ``` Log
    ERROR: Failed to execute SQL Server command:  ~ ~-- Create site boundary group ~IF  dbo.fnIsCasOrStandalonePrimary() = 1 ~BEGIN ~   PRINT N'Create site boundary group during upgrade' ~   EXEC dbo.spBuildDefaultBoundaryGroups @UserName = N'SYSTEM' ~END
    ```

    Als dit het geval is, klikt u in het knoop punt **updates en onderhoud** op **controleren op updates**en voert u de installatie van de update **opnieuw uit** .
    ***

**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

## <a name="automatically-categorize-devices-into-collections"></a><a name="dmp_category"></a>Apparaten automatisch categoriseren in verzamelingen
U kunt apparaatcategorieën maken die kunnen worden gebruikt om apparaten automatisch in apparaatsets te plaatsen wanneer u Configuration Manager gebruikt met Microsoft Intune. Gebruikers moeten dan een apparaatcategorie kiezen wanneer ze een apparaat registreren bij intune. U kunt de categorie van een apparaat ook wijzigen via de Configuration Manager-console.

**Belang rijk:** Deze functie werkt met de versie van Microsoft Intune van **juni 2016** . Zorg ervoor dat u bent bijgewerkt naar deze release voordat u deze procedures uitprobeert.

### <a name="try-it-out"></a>Probeer het nu!

### <a name="create-a-set-of-device-categories"></a>Een set apparaatcategorieën maken
1.  Vouw in de werk ruimte **activa en naleving** van de Configuration Manager-console het knoop punt **overzicht**uit en klik vervolgens op **verzamelingen van apparaten**.
2.  Klik op het tabblad **Start** in de groep **Categorieën** op **apparaatcategorieën beheren**.
3.  In het dialoog venster **apparaatcategorieën beheren** kunt u categorieën maken, bewerken of verwijderen. Probeer een nieuwe categorie te maken.

### <a name="associate-a-collection-with-a-device-category"></a>Een verzameling koppelen aan een apparaatcategorie
Wanneer u een verzameling koppelt aan een apparaatcategorie, worden alle apparaten in de door u opgegeven categorie toegevoegd aan die verzameling.
1.  Klik in het dialoog venster **Eigenschappen** voor een verzameling apparaten op **regel**  >  **Categorie apparaat**toevoegen.
2.  Selecteer in het dialoog venster **lidmaatschaps regel voor apparaat maken** de categorie die wordt toegepast op alle apparaten in de verzameling.
3.  Sluit het dialoog venster **lidmaatschaps regel** voor het maken van een apparaatcategorie en het dialoog venster Eigenschappen van verzameling.

### <a name="change-the-category-of-a-device"></a>De categorie van een apparaat wijzigen
1.  Vouw in de werk ruimte **activa en naleving** van de Configuration Manager-console het knoop punt **overzicht**uit en klik vervolgens op **apparaten**.
2.  Selecteer een apparaat in de lijst **apparaten** en klik vervolgens op het tabblad **Start** in de groep **apparaat** op **categorie wijzigen**.
3.  Kies in het dialoog venster apparaatcategorie **bewerken** de categorie die op dit apparaat moet worden toegepast en klik vervolgens op **OK**.

## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a><a name="dmp_grace"></a>Respijt periode voor afdwinging voor vereiste toepassings-en software-update-implementaties

In sommige gevallen wilt u mogelijk gebruikers meer tijd geven om vereiste toepassings implementaties of software-updates te installeren na eventuele deadlines die u hebt geconfigureerd. Dit kan meestal vereist zijn wanneer een computer gedurende lange tijd is uitgeschakeld en een groot aantal toepassings-of update-implementaties moet installeren.
Als een eind gebruiker bijvoorbeeld slechts een vakantie heeft geretourneerd, kan het zijn dat ze lang moeten wachten terwijl er achterstallige toepassings implementaties zijn geïnstalleerd.
Om dit probleem op te lossen, kunt u nu een respijt periode voor afdwinging definiëren door Configuration Manager client instellingen te implementeren voor een verzameling.

### <a name="try-it-out"></a>Probeer het nu!

Voer de volgende acties uit om de respijt periode te configureren:

1.  Configureer op de pagina **computer agent** van client instellingen de nieuwe eigenschap **respijt periode voor afdwingen na de deadline van de implementatie (uren)** met een waarde tussen **1** en **120** uur.
2.  In een nieuwe vereiste toepassings implementatie, of in de eigenschappen van een bestaande implementatie, op de pagina **planning** , selecteert u het selectie vakje **vertraging afdwingen van deze implementatie op basis van gebruikers voorkeuren**tot de respijt periode die in de client instellingen is gedefinieerd.
Alle implementaties waarvoor dit selectie vakje is ingeschakeld en die zijn bedoeld voor apparaten waarop u ook de client instelling hebt geïmplementeerd, gebruiken de respijt periode voor afdwinging.

Als u een respijt periode voor afdwinging configureert en het selectie vakje inschakelt, wordt de installatie van de toepassing geïnstalleerd in het eerste niet-zakelijke venster dat de gebruiker heeft geconfigureerd tot die respijt periode. De gebruiker kan echter nog steeds Software Center openen en de toepassing op elk gewenst moment installeren. Zodra de respijt periode is verlopen, wordt de afdwinging hersteld naar het normale gedrag voor achterstallige implementaties.
Er zijn Vergelijk bare opties toegevoegd aan de wizard software-updates implementeren, de wizard regels voor automatische implementatie en eigenschappen pagina's.

##  <a name="using-configuration-manager-as-a-managed-installer-with-device-guard"></a><a name="dmp_devg"></a>Configuration Manager gebruiken als een beheerd installatie programma met Device Guard

Device Guard is een Windows 10-functie waarbij gebruik wordt gemaakt van hardware-en software functies om strikt te bepalen wat er op het apparaat mag worden uitgevoerd.

Zie [Inleiding tot Device Guard](https://docs.microsoft.com/windows/security/threat-protection/device-guard/introduction-to-device-guard-virtualization-based-security-and-windows-defender-application-control)voor meer informatie.

In deze release kan Configuration Manager worden gebruikt in combi natie met Device Guard en [Windows AppLocker](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd723678(v=ws.10)) , zodat uitvoer bare en dll-bestanden die worden geïmplementeerd met Configuration Manager, automatisch worden vertrouwd wanneer ze afkomstig zijn van een beheerd installatie programma, wat betekent dat ze kunnen worden uitgevoerd op het doel apparaat en dat andere software niet mag worden uitgevoerd, tenzij expliciet is toegestaan om te worden uitgevoerd door andere AppLocker-regels.  

Op dit moment kan deze mogelijkheid niet worden geconfigureerd vanuit de Configuration Manager-console. Als u het beleid wilt configureren, moet u een register sleutel configureren op elke client en Windows-Services configureren op de client.
Wanneer dit is gebeurd, configureert u het AppLocker-beleids bestand. Nadat u het beleids bestand hebt geconfigureerd, kunt u het implementeren op elk compatibel client apparaat.


Net als bij alle AppLocker-beleids regels kunnen beleid met beheerde installatie Programma's in twee modi worden uitgevoerd:

- Controle modus: toepassingen zijn niet actief, maar alle toepassingen die zouden zijn geblokkeerd, worden gerapporteerd in een logboek bestand (deze worden ondersteund in een latere versie van Configuration Manager).
- Afdwinging ingeschakeld: toepassingen zijn geblokkeerd voor uitvoering.

Raadpleeg voor meer informatie de volgende artikelen:

- [Inleiding tot Device Guard](https://docs.microsoft.com/windows/security/threat-protection/device-guard/introduction-to-device-guard-virtualization-based-security-and-windows-defender-application-control)

- [Het implementatie proces van Windows Defender Application Control plannen en aan de slag gaan](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)

  ##  <a name="multiple-device-management-points-for-on-premises-mobile-device-management"></a><a name="dmp_onprem"></a>Meerdere Apparaatbeheer punten voor on-premises beheer van mobiele apparaten  
  Met Technical Preview 1606 van de on- \- premises Mobile Device Management (MDM) ondersteunt een nieuwe mogelijkheid in Windows 10 jubileum update waarmee automatisch een geregistreerd apparaat wordt geconfigureerd om meer dan één apparaatbeheerpunt beschikbaar te maken voor gebruik. Hierdoor kan het apparaat terugvallen op een ander apparaatbeheerpunt wanneer het normale gebruik niet beschikbaar is. Deze functie werkt alleen voor Pc's waarop Windows 10 jubileum update is geïnstalleerd.  

### <a name="try-it-out"></a>Probeer het nu!  

1.  Installeer meer dan één apparaatbeheerpunt in uw-hiërarchie.  

2.  Een Windows 10 jubileum update-apparaat inschrijven voor on- \- premises Mobile Device Management.  

\-Zie [mobiele apparaten beheren met on-premises infra structuur](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)voor meer informatie over het voorbereiden van uw site en het inschrijven van apparaten voor on-premises Mobile Device Management.  

## <a name="cloud-proxy-service-for-managing-clients-on-the-internet"></a><a name="cloud_proxy"></a>Cloud proxy service voor het beheren van clients op Internet

Cloud proxy service biedt een eenvoudige manier om Configuration Manager-clients op het Internet te beheren. De service, die is geïmplementeerd voor Microsoft Azure en waarvoor een Azure-abonnement is vereist, maakt verbinding met uw on-premises Configuration Manager-infra structuur met behulp van een nieuwe functie genaamd het connector punt van de Cloud proxy. Zodra het volledig is geïmplementeerd en geconfigureerd, hebben clients toegang tot on-premises Configuration Manager site systeem rollen, ongeacht of ze zijn verbonden met het interne particuliere netwerk of via internet.

U gebruikt de Configuration Manager-console om de service te implementeren in azure, de rol van de Cloud proxy connector toe te voegen en site systeem rollen te configureren om Cloud proxy verkeer toe te staan. Cloud proxy service biedt momenteel alleen ondersteuning voor de rollen beheer punt, distributie punt en software-update punt.

Client certificaten en SSL-certificaten (Secure Sockets Layer) zijn vereist voor de verificatie van computers en het versleutelen van de communicatie tussen de verschillende lagen van de service. Client computers ontvangen doorgaans een client certificaat via het afdwingen van groeps beleid. Voor het versleutelen van het verkeer tussen clients en de site systeem server die als host fungeert voor de rollen, moet u een aangepast SSL-certificaat maken op basis van de CA. Naast deze twee typen certificaten moet u ook een beheer certificaat instellen op Azure waarmee Configuration Manager Cloud proxy service kunt implementeren.  

### <a name="requirements-for-cloud-proxy-service-in-tp-1606"></a>Vereisten voor Cloud proxy service in TP 1606
- Client computers en de site systeem server waarop het Cloud proxy connector punt wordt uitgevoerd.
- Aangepaste SSL-certificaten van de interne certificerings instantie: wordt gebruikt voor het versleutelen van de communicatie van de client computers en het verifiëren van de identiteit van de Cloud proxy service.
- Azure-abonnement voor Cloud Services.
- Azure-beheer certificaat: wordt gebruikt voor het verifiëren van Configuration Manager met Azure.

### <a name="limitations-of-cloud-proxy-service-in-tp-1606"></a>Beperkingen van Cloud proxy service in TP 1606

- Ondersteunt alleen de rollen beheer punt, distributie punt en software-update punt.
- Gebruikers beleid wordt niet ondersteund.
- Kan niet worden gebruikt met [on-premises Mobile Device Management](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) in Configuration Manager.
- Alleen ondersteund op het open bare Cloud platform van Azure.


### <a name="try-it-out"></a>Probeer het nu!

Het proces voor het implementeren van Cloud proxy service omvat de volgende stappen:

1. Een aangepast SSL-certificaat maken en uitgeven voor Cloud proxy service.
1. De hoofdmap van het client certificaat exporteren.
2. Upload het beheer certificaat naar Azure.
3. Cloud proxy service instellen in de Configuration Manager-console.
4. Configureer de primaire site voor het gebruik van verificatie op basis van client certificaten.
5. Voeg het Cloud proxy connector punt toe aan uw site.
6. Configureer de site systeem rollen om Cloud proxy verkeer te accepteren.

In de volgende secties vindt u meer informatie over het uitvoeren van deze stappen.

#### <a name="create-a-custom-ssl-certificate"></a>Een aangepast SSL-certificaat maken

U kunt op dezelfde manier een aangepast SSL-certificaat voor Cloud proxy service maken als voor een distributie punt in de Cloud. Volg de instructies voor [het implementeren van het service certificaat voor distributie punten in de Cloud,](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012) maar u moet de volgende dingen doen:

* Geef bij het instellen van het nieuwe certificaat sjabloon de machtigingen **lezen** en **registreren** op voor de beveiligings groep die u hebt ingesteld voor Configuration Manager-servers.

#### <a name="export-the-client-certificates-root"></a>De hoofdmap van het client certificaat exporteren

De eenvoudigste manier om de hoofdmap van de client certificaten die worden gebruikt op het netwerk te maken, is door een client certificaat te openen op een van de computers die lid zijn van het domein en deze te kopiëren.

>[!NOTE]
>Client certificaten zijn vereist op elke computer die u wilt beheren met de Cloud proxy service en op de site systeem server die als host fungeert voor het Cloud proxy connector punt. Zie [het client certificaat voor Windows-computers implementeren](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012)als u een client certificaat aan een van deze computers wilt toevoegen.

1. Typ in het venster uitvoeren **MMC** en druk op ENTER.
2. Klik in het menu bestand in de beheer console op **module toevoegen/verwijderen...**.
3. Klik in het dialoog venster modules toevoegen of verwijderen op **certificaten**, klik op **toevoegen >**, klik op **computer account**, klik op **volgende**, klik op **lokale computer**en klik vervolgens op **volt ooien**. Klik op **OK** om het dialoogvenster te sluiten.
4. Ga naar **certificaten > persoonlijke > certificaten**.
5. Dubbel klik op het certificaat voor client verificatie op de computer, klik op het tabblad Certificeringspad en dubbel klik op de basis instantie (boven aan het pad).
6.  Klik op het tabblad Details en klik vervolgens op **kopiëren naar bestand...**.
7. Voltooi de wizard Certificaat exporteren door de standaard certificaat indeling te gebruiken. Noteer de naam en locatie van het basis certificaat dat u maakt. U hebt deze nodig voor het configureren van Cloud proxy service in een latere stap.

#### <a name="upload-the-management-certificate-to-azure"></a>Het beheer certificaat uploaden naar Azure

Er is een Azure-beheer certificaat vereist om Configuration Manager toegang te krijgen tot de Azure API en de Cloud proxy service te configureren. Raadpleeg de volgende artikelen in de Azure-documentatie voor meer informatie en instructies voor het uploaden van een beheer certificaat:
- [Overzicht van certificaten voor Azure Cloud Services](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)
- [Een Azure Management API Management-certificaat uploaden](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/).

Zorg ervoor dat u de abonnements-ID kopieert die is gekoppeld aan het beheer certificaat. U hebt deze nodig voor het configureren van Cloud proxy service in de Configuration Manager-console.

#### <a name="set-up-cloud-proxy-service"></a>Cloud proxy service instellen

1. Ga in de Configuration Manager-console naar **beheer > Cloud Services > Cloud proxy service**.
2. Klik op **Cloud proxy service maken**.
3. Voer in de wizard Cloud proxy service maken uw Azure-abonnements-ID in (overgenomen van de Azure-beheer Portal), klik op Bladeren en selecteer het certificaat bestand dat u hebt gebruikt voor het uploaden als een Azure-beheer certificaat. Klik op **Volgende**. Wacht even totdat de console verbinding maakt met Azure.
4. Vul de extra gegevens in de wizard in:
    - Geef de persoonlijke sleutel (. pfx-bestand) op die u hebt geëxporteerd uit het aangepaste SSL-certificaat.
    - Geef het basis certificaat op dat is geëxporteerd van het client certificaat.
    - Geef dezelfde service naam FQDN op die u hebt gebruikt tijdens het maken van het nieuwe certificaat sjabloon.
    - Schakel het selectie vakje naast het **intrekken van client certificaten te controleren** (tenzij u uw CRL-gegevens openbaar publiceert).
    - Klik op **volgende** wanneer u klaar bent.
5. Controleer de instellingen en klik op **volgende**. Configuration Manager begint met het instellen van de service. Wanneer de wizard is voltooid, kunt u op **sluiten**klikken. het duurt echter tussen vijf tot 15 minuten om de service volledig in te richten in Azure. Controleer de kolom **status** voor de zojuist ingestelde Cloud proxy service om te bepalen wanneer de service gereed is.

#### <a name="configure-primary-site-for-client-certification-authentication"></a>Primaire site configureren voor verificatie van client certificering

1. Ga in de Configuration Manager-console naar **beheer > site configuratie > sites**.
2. Selecteer de primaire site voor de clients die u wilt beheren via de Cloud proxy service en klik op **Eigenschappen**.
3. Schakel op het tabblad communicatie client computer van het eigenschappen venster van de primaire site het selectie vakje naast **PKI-client certificaat (client verificatie) gebruiken in wanneer beschikbaar**.
4. Zorg ervoor dat u het selectie vakje naast clients inschakelt **de certificaatintrekkingslijst (CRL) voor site systemen controleren**. Deze optie is alleen vereist als u uw CRL openbaar publiceert.
5. Klik op **OK**.

#### <a name="add-the-cloud-proxy-connector-point"></a>Het Cloud proxy connector-punt toevoegen

Het Cloud proxy connector punt is een nieuwe site systeemrol voor het communiceren met Cloud proxy service. Volg de instructies in [site systeem rollen toevoegen voor Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md)om het Cloud proxy connector-punt toe te voegen.

#### <a name="configure-roles-for-cloud-proxy-traffic"></a>Rollen voor Cloud proxy verkeer configureren

De laatste stap bij het instellen van de Cloud proxy service is het configureren van de site systeem rollen om Cloud proxy verkeer te accepteren. Voor de Tech Preview 1606 worden alleen de rollen beheer punt, distributie punt en software-update punt ondersteund voor Cloud proxy service. U moet elke rol afzonderlijk configureren.

1. Ga in de Configuration Manager-console naar **beheer > site configuratie > servers en site systeem rollen**.
2. Klik op de site systeem server voor de rol die u wilt configureren voor Cloud proxy verkeer.
3. Klik op de rol en klik vervolgens op **Eigenschappen**.
4. Kies in het venster Eigenschappen van rol onder client verbindingen **https**, schakel het selectie vakje naast **Configuration Manager Cloud proxy verkeer toestaan**in en klik vervolgens op **OK**. Herhaal deze stappen voor de resterende rollen.

#### <a name="check-status-on-a-client-on-the-internet"></a>Status controleren op een client op Internet

Nadat de service en rollen volledig zijn geconfigureerd, krijgen interne clients de locatie van de Cloud proxy service op de volgende locatie aanvraag. Clients met bijgewerkte locatie gegevens kunnen vervolgens communiceren met Configuration Manager op internet. De polling cyclus voor locatie aanvragen is elke 24 uur. Als u niet wilt wachten op de normale geplande locatie aanvraag, kunt u de aanvraag afdwingen door de SMS agent host-service (ccmexec. exe) opnieuw te starten op de computer.

Nadat clients de nieuwe locatie-informatie voor de Cloud proxy service hebben, kunt u de status controleren van clients die zich niet meer op het interne particuliere netwerk bevinden, maar wel over Internet toegang hebben. U kunt ook verkeer op Cloud proxy service controleren door naar **beheer > te gaan Cloud Services > Cloud proxy service**, de service in het deel venster met de lijst te selecteren en de verkeers gegevens in het detail venster weer te geven.   

## <a name="manage-the-office-365-client-agent-in-configuration-manager"></a><a name="manage_o365"></a>Office 365-clientagent beheren in Configuration Manager  

Het starten van Technical Preview 1606, kunt u een instelling voor een Configuration Manager client agent gebruiken in plaats van groeps beleid, zodat Office 365-clients updates van Configuration Manager kunnen ontvangen. Nadat u deze instelling hebt geconfigureerd en Office 365-updates hebt geïmplementeerd, communiceert de Configuration Manager-client agent met de Office 365-client agent om Office 365-updates te downloaden vanaf een distributie punt en te installeren. Configuration Manager maakt ook inventarisatie van de instelling van de client agent.

Zie [Office 365 ProPlus-updates beheren](../../sum/deploy-use/manage-office-365-proplus-updates.md)voor meer informatie.

### <a name="set-the-configuration-manager-client-setting-to-manage-the-office-365-client-agent"></a>Stel de Configuration Manager client instelling in om de Office 365-client agent te beheren
1.  Klik in de Configuration Manager-console op **beheer**  >  **overzicht**  >  **client instellingen**.
2. Open de juiste Apparaatinstellingen om de client agent in te scha kelen. Zie [client instellingen configureren](../../core/clients/deploy/configure-client-settings.md)voor meer informatie over standaard-en aangepaste client instellingen.
3. Klik op **software-updates** en selecteer **Ja** voor de instelling **beheer van de Office 365-client agent inschakelen** .  


## <a name="the-osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a><a name="osdpreservedriveletter"></a>Takenreeksvariabele OSDPreserveDriveLetter is afgeschaft
De taken reeks variabele OSDPreserveDriveLetter bepaalt of de taken reeks de stationsletter gebruikt die is vastgelegd in het WIM-bestand van de installatie kopie van het besturings systeem wanneer die installatie kopie wordt toegepast op een doel computer.
- Deze taken reeks variabele is afgeschaft in Technical Preview 1606.

Tijdens de implementatie van een besturings systeem bepaalt Windows Setup nu de beste stationsletter die moet worden gebruikt (meestal C:). Als u een ander station wilt opgeven, kunt u de locatie wijzigen in de taken reeks stap besturings systeem Toep assen. Ga naar de **locatie selecteren waar u dit besturings systeem wilt Toep assen** , selecteer **specifieke logische stationsletter**en kies het station dat u wilt gebruiken. Er moet een station zijn dat is toegewezen aan de letter die u kiest op de doel computer. 

## <a name="changes-for-the-updates-and-servicing-node"></a><a name="updatesandservicing"></a>Wijzigingen voor het knooppunt Updates en onderhoud
Met Technical Preview 1606 zijn verschillende wijzigingen geïntroduceerd die van toepassing zijn op updates en onderhoud in de Configuration Manager-console:
- **Wijziging van knooppunt naam:**

    In de werk ruimte **bewaking** is de naam van het knoop punt voor **site onderhoud** gewijzigd in de **status updates en onderhoud**.
- **Meer installatie status:**

    Wanneer u de update-installatie status voor een site bekijkt, worden in de console nu afzonderlijke details weer gegeven voor de volgende acties:
    - **Downloaden** (dit is alleen van toepassing op de site op het hoogste niveau waar de site systeemrol voor het service aansluitpunt is geïnstalleerd).
    - **Replicatie**
    - **Vereistencontrole**
    - **Installatie**

  Daarnaast vindt u hier meer gedetailleerde informatie over elke stap, zoals in het logboek bestand dat u kunt weer geven voor meer informatie.  
-   **Nieuwe optie voor het opnieuw proberen van vereiste fouten:**

    In de werk ruimten **beheer** en **bewaking** bevat het knoop punt **updates en onderhoud** een nieuwe knop op het lint met de naam **waarschuwingen over vereisten negeren**.

    Wanneer u updates installeert zonder gebruik te maken van de optie om waarschuwingen over vereisten te negeren (vanuit de wizard updates) en de installatie van de update stopt met de status **vereisten-waarschuwing**, kunt u de **waarschuwingen voor vereisten negeren** van het lint selecteren om een automatische voortzetting van die update-installatie te activeren waarbij de waarschuwingen voor vereisten worden genegeerd.  



- **Overzichtelijke weer gave van updates:**

    Wanneer u het knoop punt **updates en onderhoud** bekijkt, ziet u nu alleen de meest recent geïnstalleerde update en eventuele nieuwe updates die u kunt installeren. Als u eerder geïnstalleerde updates wilt weer geven, klikt u op de knop nieuw **geschiedenis** die wordt weer gegeven op het lint.  

-   **De naam van de optie is gewijzigd voor de pre-productie:**

    In het knoop punt updates en onderhoud is de naam van de knop wat **client opties** is, nu hernoemd voor het **promo veren van de pre-productie client**.
