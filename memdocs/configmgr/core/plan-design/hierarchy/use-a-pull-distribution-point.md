---
title: Pull-distributie punt
titleSuffix: Configuration Manager
description: Meer informatie over configuraties en beperkingen voor het gebruik van een pull-distributie punt met Configuration Manager.
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c243897a4c52eff04263325b998c4b23d6b3dde4
ms.sourcegitcommit: ad4b3e4874a797b755e774ff84429b5623f17c5c
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/27/2020
ms.locfileid: "82166584"
---
# <a name="use-a-pull-distribution-point-with-configuration-manager"></a>Een pull-distributie punt gebruiken met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Wanneer u inhoud distribueert naar een standaard distributiepunt in de Configuration Manager-console, duwt de site server de inhoud naar het distributie punt. Een pull-distributie punt haalt inhoud op door het te downloaden van een bron locatie zoals een client.  

Wanneer u inhoud distribueert naar een groot aantal distributie punten, kunnen pull-distributie punten de verwerkings belasting op de site server verlagen. Ze kunnen ook de overdracht van inhoud naar elke server versnellen. Normaal gesp roken verzendt het onderdeel Distribution Manager op de site server inhoud naar elk distributie punt. In plaats daarvan offloadt de site het proces van het overdragen van de inhoud naar de pull-distributie punten.  

U kunt afzonderlijke distributie punten configureren als pull-distributie punten. Geef voor elk pull-distributie punt een of meer bron distributiepunten op waarvan het inhoud kan ophalen. Een pull-distributie punt kan alleen inhoud downloaden van een distributie punt dat u opgeeft als een bron distributiepunt.

Wanneer u inhoud distribueert naar een pull-distributie punt in de-console, verzendt de site server een melding. Het pull-distributie punt downloadt vervolgens de inhoud van een bron distributiepunt. Een pull-distributie punt beheert de overdracht van inhoud door te downloaden vanaf een distributie punt dat al een kopie van de inhoud heeft.  

Pull-distributie punten ondersteunen dezelfde configuraties en functionaliteit als typische distributie punten. Een pull-distributie punt ondersteunt bijvoorbeeld:

- Multi cast-en PXE-configuraties
- Validatie van inhoud
- Inhoudsdistributie op aanvraag
- HTTP-of HTTPS-communicatie van clients
- Dezelfde certificaat opties als andere distributie punten
- Afzonderlijk of als een lid van een distributiepunten groep beheren  

Een pull-distributie punt configureren wanneer u het distributie punt installeert. Nadat u een distributie punt hebt gemaakt, moet u dit configureren als een pull-distributie punt door de functie-eigenschappen te bewerken. Zie [pull-distributie punt](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pull)voor meer informatie over het inschakelen van een distributie punt als een pull-distributie punt.  

Verwijder de configuratie voor een pull-distributie punt door de eigenschappen van het distributie punt te bewerken. Wanneer u de configuratie als een pull-distributie punt verwijdert, wordt de normale bewerking opnieuw uitgevoerd. De site server beheert toekomstige overdrachten van inhoud naar het distributie punt.  

## <a name="distribution-process"></a>Distributie proces

Wanneer u inhoud distribueert naar een pull-distributie punt, vindt de volgende reeks gebeurtenissen plaats:

- Wanneer u inhoud distribueert naar een pull-distributie punt in de-console, controleert het onderdeel package overzet Manager op de site server de site database om te bevestigen of de inhoud beschikbaar is op een bron distributiepunt. Als er niet kan worden bevestigd dat de inhoud zich op een bron distributiepunt voor het pull-distributie punt bevindt, wordt de controle om de 20 minuten herhaald totdat de inhoud beschikbaar is.  

- Wanneer door Package Transfer Manager wordt bevestigd dat de inhoud beschikbaar is, meldt dit aan het pull-distributiepunt dat de inhoud kan worden gedownload. Als deze melding mislukt, worden nieuwe pogingen gedaan op basis van de **instellingen voor opnieuw proberen** van het software distributie onderdeel voor pull-distributie punten. Wanneer het pull-distributie punt deze melding ontvangt, probeert het de inhoud te downloaden vanaf de bijbehorende bron distributiepunten.  

- Terwijl het pull-distributie punt de inhoud downloadt, pollt de package overboeking Manager de status op basis van de **polling-instellingen** voor het software distributie onderdeel voor pull-distributie punten.  Wanneer het pull-distributie punt het downloaden van inhoud heeft voltooid, verzendt dit deze status naar een beheer punt.  

## <a name="configure-site-component-settings"></a>Instellingen voor site onderdelen configureren

Wanneer u een pull-distributie punt gebruikt, controleert en configureert u de volgende instellingen voor het site onderdeel:  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** .  

2. Selecteer de site. Selecteer in het lint **site onderdelen configureren**en selecteer **software distributie**.  

3. Schakel over naar het **pull-distributie punt** tabblad.  

4. Controleer de volgende waarden in de groep **instellingen voor opnieuw proberen** :  

    - **Aantal nieuwe pogingen**: het aantal keren dat de package overboeking Manager probeert het pull-distributie punt te melden om de inhoud te downloaden. Na dit aantal pogingen wordt de overdracht geannuleerd door package overdracht Manager. Deze waarde is standaard 30.  

    - **Vertraging voor opnieuw proberen (minuten)**: het aantal minuten dat de package overboeking Manager tussen pogingen wacht. Deze waarde is standaard 20.  

5. Controleer de volgende waarden in de groep **status polling-instellingen** :  

    - **Aantal polls**: het aantal keren dat de package overboeking manager contact opneemt met het pull-distributie punt om de taak status op te halen. Als dit aantal keer wordt geprobeerd voordat de taak is voltooid, annuleert de package overboeking Manager de overdracht. Deze waarde is standaard 72.

    - **Vertraging voor opnieuw proberen (minuten)**: het aantal minuten dat de package overboeking Manager tussen pogingen wacht. Deze waarde is standaard 60.

    > [!NOTE]  
    >  Wanneer de package overboeking Manager een taak annuleert omdat deze het aantal polling pogingen overschrijdt, blijft het pull-distributie punt de inhoud downloaden. Wanneer het pull-distributie punt is voltooid, wordt het juiste status bericht verzonden. de console geeft de nieuwe status weer.  

## <a name="limitations"></a>Beperkingen

- U kunt een Cloud distributiepunt niet configureren als een pull-distributie punt.  

- U kunt de rol distributie punt niet configureren op een site server als een pull-distributie punt.  

- De configuratie voor het pull-distributiepunt wordt door de configuratie voor voorbereide inhoud overschreven. Als u de optie inschakelt om **Dit distributie punt in te scha kelen voor voor bereide inhoud** op een pull-distributie punt, wordt gewacht op de inhoud. Er wordt geen inhoud opgehaald van het bron distributiepunt. Net als een standaard distributie punt dat is ingeschakeld voor voor bereide inhoud, ontvangt het geen inhoud van de site server. Zie voor [bereide inhoud](manage-network-bandwidth.md#BKMK_PrestagingContent)voor meer informatie.  

- Een pull-distributie punt maakt geen gebruik van schema-of frequentie limiet configuraties. Wanneer u een eerder geïnstalleerd distributie punt configureert als een pull-distributie punt, worden configuraties voor plannings-en frequentie limieten opgeslagen, maar niet gebruikt. Als u later de configuratie van het pull-distributie punt verwijdert, worden de schema-en frequentie limiet configuraties geïmplementeerd zoals eerder geconfigureerd.  

    > [!NOTE]  
    >  De tabbladen **schema** en **frequentie limieten** zijn niet zichtbaar in de eigenschappen van het distributie punt.  

- Pull-distributie punten gebruiken niet de instellingen op het tabblad **Algemeen** van de **Eigenschappen van software distributie onderdelen** van elke site. Deze instellingen omvatten **gelijktijdige distributie** en **multi cast-poging**.  

- Als u inhoud wilt overdragen vanaf een bron distributiepunt in een extern forest, installeert u de Configuration Manager-client op het pull-distributie punt. Configureer ook een netwerk toegangs account dat toegang heeft tot het bron distributiepunt. Als u de site optie inschakelt voor het **gebruik van door Configuration Manager gegenereerde certificaten voor HTTP-site systemen**, hebt u geen netwerk toegangs account nodig.<!--1358228-->  

- Als het pull-distributie punt ook een Configuration Manager client, moet de client versie hetzelfde zijn als de Configuration Manager-site die het pull-distributie punt installeert. Het pull-distributie punt gebruikt de CCMFramework die gebruikelijk is voor het pull-distributie punt en de Configuration Manager-client.  

## <a name="about-source-distribution-points"></a>Brondistributiepunten  

Wanneer u het pull-distributie punt configureert, geeft u een of meer bron distributiepunten op:  

- De wizard geeft alleen distributie punten weer die in aanmerking komen voor bron distributiepunten.  

- Een pull-distributiepunt kan worden opgegeven als een brondistributiepunt voor een ander pull-distributiepunt.  

- Alleen distributie punten die ondersteuning bieden voor HTTP, kunnen worden opgegeven als bron distributiepunten wanneer u de Configuration Manager-console gebruikt.  

- Gebruik de Configuration Manager SDK om een bron distributiepunt op te geven dat is geconfigureerd voor HTTPS. Als u een bron distributiepunt wilt gebruiken dat is geconfigureerd voor HTTPS, installeert u de Configuration Manager-client op het pull-distributie punt.  

- Als uw externe kant oren een betere verbinding met internet hebben of als u de belasting van uw WAN-koppelingen wilt reduceren, gebruikt u een [Cloud distributiepunt](use-a-cloud-based-distribution-point.md) in Microsoft Azure als bron. Het pull-distributie punt heeft Internet toegang nodig om te kunnen communiceren met Microsoft Azure. De inhoud moet worden gedistribueerd naar het bron-Cloud distributiepunt.<!--1321554-->  

    > [!Note]  
    > Met deze functie worden kosten in rekening gebracht voor uw Azure-abonnement voor gegevens opslag en netwerk uitgaand verkeer. Zie de kosten voor het [gebruik van een Cloud distributiepunt](use-a-cloud-based-distribution-point.md#bkmk_cost)voor meer informatie.  

> [!Tip]  
> Wanneer een pull-distributiepunt inhoud downloadt vanaf een brondistributiepunt, wordt dat pull-distributiepunt in de kolom **Gebruikte (unieke) clients** van het rapport **Overzicht van gebruik van distributiepunten** geteld als een client.  

### <a name="source-priorities"></a>Bron prioriteiten

- Wijs een afzonderlijke prioriteit toe aan elk bron distributiepunt of wijs meerdere bron distributiepunten toe aan dezelfde prioriteit.  

- De prioriteit bepaalt de volg orde waarin het pull-distributie punt inhoud aanvraagt vanaf de bron distributiepunten.  

- Pull-distributiepunten maken eerst contact met een brondistributiepunt met de laagste waarde voor de prioriteit. Als er meerdere bron distributiepunten met dezelfde prioriteit zijn, selecteert het pull-distributie punt wille keurig een van de bronnen met die prioriteit.  

- Als de inhoud niet beschikbaar is op een geselecteerde bron, probeert het pull-distributie punt de inhoud te downloaden vanaf een ander distributie punt met dezelfde prioriteit.  

- Als geen van de distributie punten met een bepaalde prioriteit de inhoud heeft, probeert het pull-distributie punt de inhoud te downloaden vanaf een bron distributiepunt met het niveau van de volgende prioriteit. Deze zoek opdracht wordt voortgezet totdat de inhoud zich bevindt.

- Als geen van de toegewezen bron distributiepunten de inhoud heeft, wacht het pull-distributie punt 30 minuten en wordt het proces vervolgens opnieuw gestart.  

## <a name="inside-the-pull-distribution-point"></a>In het pull-distributie punt

- Pull-distributie punten gebruiken het onderdeel **CCMFramework** om de overdracht van inhoud te beheren. De Configuration Manager-client bevat dit onderdeel.  

- Wanneer u het pull-distributie punt inschakelt, installeert de site **pulldp. msi**. Dit installatie programma voegt ook het onderdeel CCMFramework toe. De Configuration Manager-client is niet vereist voor het Framework.  

- Nadat het pull-distributie punt is geïnstalleerd, wordt in eerste instantie de **CCMExec** -service gebruikt om te werken.  

- Wanneer het pull-distributie punt inhoud overdraagt, maakt het gebruik van de **Background Intelligent Transfer service** (bits) die zijn ingebouwd in Windows. Voor een pull-distributie punt is het niet vereist dat u de BITS-extensie voor de IIS-server installeert.<!--sms.503672 -Clarified BITS use-->

- Zie de volgende logboek bestanden op het pull-distributie punt voor operationele details:  

  - **DataTransferService.log**
  - **PullDP.log**

> [!TIP]
> Als er HTTP 403-fouten in de logboek bestanden worden weer geven nadat u een pull-distributie punt hebt toegevoegd, moet u de volgende wijziging aanbrengen:
>
> 1. Stel op het bron distributiepunt de volgende register waarde in:`HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL, ClientAuthTrustMode = 2 (REG_DWORD)`
> 1. Start de bron distributiepunt server opnieuw op.
>
> Vervolgens moet het pull-distributie punt beginnen met het downloaden van inhoud van de bron. Zie [overzicht van TLS-SSL (Schannel-SSP)](https://docs.microsoft.com/windows-server/security/tls/what-s-new-in-tls-ssl-schannel-ssp-overview)voor meer informatie over deze register sleutel.<!-- SCCMDocs#1973 -->

## <a name="see-also"></a>Zie ook  

[Basisconcepten voor inhoudsbeheer](fundamental-concepts-for-content-management.md)
