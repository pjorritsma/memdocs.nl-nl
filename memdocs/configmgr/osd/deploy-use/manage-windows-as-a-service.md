---
title: Windows als een service beheren
titleSuffix: Configuration Manager
description: Bekijk de status van Windows as a Service (WaaS) met behulp van Configuration Manager, maak onderhouds plannen voor het distribueren van implementatie ringen en bekijk waarschuwingen wanneer Windows 10 clients bijna de ondersteuning ondervinden.
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: da1e687b-28f6-43c4-b14a-ff2b76e60d24
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9a682ec0b3d438a26429486f119d641fd150404f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710837"
---
# <a name="manage-windows-as-a-service-using-configuration-manager"></a>Windows als een service beheren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In Configuration Manager kunt u de status van Windows als een service (WaaS) in uw omgeving weer geven. Maak onderhouds plannen om implementatie ringen te maken, en zorg ervoor dat Windows 10-systemen up-to-date blijven wanneer er nieuwe builds worden uitgebracht. U kunt ook waarschuwingen weer geven wanneer Windows 10-clients bijna de ondersteuning ondervinden voor het semi-Annual-kanaal bouwen.

Zie [overzicht van Windows als een service](/windows/deployment/update/waas-overview#servicing-channels)voor meer informatie over Windows 10-onderhouds opties.

Gebruik de volgende secties voor het beheren van Windows als een service.

## <a name="prerequisites"></a><a name="BKMK_Prerequisites"></a>Vereisten

Als u gegevens in het Windows 10-onderhouds dashboard wilt bekijken, moet u de volgende acties uitvoeren:

- Windows 10-computers moeten Configuration Manager software-updates gebruiken met Windows Server Update Services (WSUS) voor software-update beheer. Wanneer computers Windows Update gebruiken voor bedrijven (of Windows insiders) voor het beheer van software-updates, wordt de computer niet geëvalueerd in Windows 10-onderhouds plannen. Zie [Integratie met Windows Update voor bedrijven in Windows 10](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)voor meer informatie.

- Een ondersteunde WSUS-versie gebruiken:
  - WSUS-10.0.14393 (rol in Windows Server 2016)
  - WSUS-10.0.17763 (rol in Windows Server 2019) (hiervoor is Configuration Manager 1810 of hoger vereist)
  - WSUS 6,2 en 6,3 (rol in Windows Server 2012 en Windows Server 2012 R2)
    - [Kb 3095113 en kb 3159706 (of een equivalente update) moeten worden geïnstalleerd](../../sum/plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012) op WSUS 6,2 en 6,3.

- Schakel heartbeat-detectie in. De gegevens die worden weergegeven in het Windows 10-onderhoudsdashboard worden gevonden door middel van detectie. Zie [Heartbeat-detectie configureren](../../core/servers/deploy/configure/configure-discovery-methods.md#BKMK_ConfigHBDisc)voor meer informatie.

    De volgende Windows 10-kanalen en buildgegevens worden gedetecteerd en opgeslagen in de volgende kenmerken:  

    - **Gereedheids vertakking van het besturings systeem**: Hiermee geeft u het kanaal van het besturings systeem op. Bijvoorbeeld: **0** = Semi-Annual-kanaal-doel (geen updates uitstellen), **1** = Semi-Annual-kanaal (updates uitstellen), **2** = Long-term Servicing Channel (LTSC)

    - **Build van besturings systeem**: Hiermee geeft u de build van het besturings systeem op. Bijvoorbeeld **10.0.10240** (RTM) of **10.0.10586** (versie 1511)

- Het service aansluitpunt moet zijn geïnstalleerd en geconfigureerd voor de modus voor **online en permanente verbinding** om gegevens te bekijken op het Windows 10-onderhouds dashboard. Wanneer u zich in de offline modus bevindt, ziet u geen gegevens updates in het dash board totdat u Configuration Manager onderhouds updates ontvangt. Zie [about the Service Connection Point](../../core/servers/deploy/configure/about-the-service-connection-point.md)(Engelstalig) voor meer informatie.

- Internet Explorer 9 of hoger moet zijn geïnstalleerd op de computer waarop de Configuration Manager-console wordt uitgevoerd.

- Software-updates moeten zijn geconfigureerd en gesynchroniseerd. Selecteer de classificatie **upgrades** en synchroniseer software-updates voordat er upgrades van Windows 10-functies beschikbaar zijn in de Configuration Manager-console. Zie voor meer informatie [voor bereiding op het beheer van software-updates](../../sum/get-started/prepare-for-software-updates-management.md).

- Controleer vanaf Configuration Manager versie 1902 of de [client instelling](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority) **thread-prioriteit opgeven voor functie-updates is ingeschakeld** , zodat deze geschikt is voor uw omgeving.

- Controleer vanaf Configuration Manager versie 1906 de [client instelling](../../core/clients/deploy/about-client-settings.md#bkmk_du) **dynamische updates voor functie-updates inschakelen** om ervoor te zorgen dat deze geschikt is voor uw omgeving. <!--4062619-->

## <a name="windows-10-servicing-dashboard"></a><a name="BKMK_ServicingDashboard"></a> Windows 10-onderhoudsdashboard

In het Windows 10-onderhoudsdashboard vindt u onder andere informatie over Windows 10-computers in uw omgeving, actieve onderhoudsplannen en informatie over de compatibiliteit. Voor de weergave van de gegevens in het Windows 10-onderhoudsdashboard moet het serviceaansluitpunt zijn geïnstalleerd. Het dashboard bevat de volgende tegels:

- **Tegel Windows 10-gebruik**: geeft een overzicht van de open bare builds van Windows 10. Windows insiders-builds worden vermeld als **andere** , evenals de builds die nog niet bekend zijn bij uw site. Het service aansluitpunt downloadt meta gegevens die deze informatie over de Windows-builds ontvangen. vervolgens worden deze gegevens vergeleken met de detectie gegevens.

- **Tegel Windows 10-ringen**: geeft een uitsplitsing van de status van Windows 10 per kanaal en gereedheid. Het LTSC-segment bevat alle versies van LTSC. De eerste tegel onderbreekt de specifieke versies, bijvoorbeeld Windows 10 LTSC 2015.

- **Tegel service plan maken**: biedt een snelle manier om een onderhouds plan te maken. U geeft de naam op, verzameling (alleen de tien belangrijkste verzamelingen worden weer gegeven op grootte, kleinste eerst), implementatie pakket (alleen de tien meest recent gewijzigde pakketten worden weer gegeven) en de gereedheids status. Voor de overige instellingen worden de standaardwaarden gebruikt. Klik op **Geavanceerde instellingen** om de wizard onderhouds plan maken te starten. hier kunt u alle instellingen voor het service plan configureren.

- **De tegel Verlopen**: geeft het percentage apparaten weer met een versie van Windows 10 waarvan de levensduur is verstreken. Configuration Manager bepaalt het percentage van de meta gegevens dat het service aansluitpunt downloadt en vergelijkt met de detectie gegevens. Een build waarvan het einde van de levens duur is verstreken, ontvangt geen maandelijkse cumulatieve updates meer, zoals beveiligings updates. De computers in deze categorie moeten worden bijgewerkt naar de volgende buildversie. Configuration Manager wordt naar boven afgerond op het dichtstbijzijnde gehele getal. Als u bijvoorbeeld 10.000 computers hebt en slechts één op een verlopen build, wordt op de tegel 1% weer gegeven.

- **De tegel Verloopt binnenkort**: geeft het percentage computers weer waarvan het einde van de levensduur nadert (binnen ongeveer vier maanden), vergelijkbaar met de tegel **Verlopen** . Configuration Manager wordt naar boven afgerond op het dichtstbijzijnde gehele getal.

- **De tegel Waarschuwingen**: geeft de actieve waarschuwingen weer.

- **Tegel bewaking service plan**: Hiermee geeft u de onderhouds plannen weer die u hebt gemaakt en een overzicht van de compatibiliteit voor elk. Deze tegel geeft u een snel overzicht van de huidige status van de implementaties van het onderhouds plan. Als een eerdere implementatiering voldoet aan de verwachtingen voor compatibiliteit, kunt u een later onderhoudsplan (implementatiering) selecteren en op **Nu implementeren** klikken in plaats van te wachten op de automatische activering van de onderhoudsplanregels.

- De **tegel Windows 10-builds**: weer geven is een tijd lijn met een vaste afbeelding die een overzicht geeft van de Windows 10-builds die momenteel zijn uitgebracht en die een algemeen idee hebben van het samen stellen van een overgang naar verschillende statussen. Deze tegel is verwijderd vanaf Configuration Manager versie 1902, omdat meer gedetailleerde informatie wordt aangeboden in het [dash board voor product levenscyclus](../../core/clients/manage/asset-intelligence/product-lifecycle-dashboard.md). <!--3446861-->

> [!IMPORTANT]
> De gegevens die in het Windows 10-onderhoudsdashboard worden weergegeven (zoals de ondersteuningslevenscyclus voor versies van Windows 10) dienen uw gemak en zijn alleen voor intern gebruik in uw bedrijf bestemd. U moet niet alleen afgaan op deze gegevens wanneer u de compatibiliteit van updates controleert. Controleer de juistheid van de gegevens die wordt weergegeven.

## <a name="drill-through-required-updates"></a>Bekijk de vereiste updates
<!--4224414-->
*(Geïntroduceerd in versie 1906)*

U kunt inzoomen op nalevings statistieken om te zien voor welke apparaten een specifieke Windows 10-functie-update is vereist. Als u de lijst met apparaten wilt weer geven, hebt u machtigingen nodig voor het weer geven van updates en de verzamelingen waartoe de apparaten behoren. Inzoomen op de apparaten lijst:

1. Ga naar **software bibliotheek** > **Windows 10 onderhoud** > **alle Windows 10-updates**.
1. Selecteer een update die vereist is voor ten minste één apparaat.
1. Ga naar het tabblad **samen vatting** en zoek het cirkel diagram onder **Statistieken**.
1. Selecteer de **weer gave vereiste** Hyper link naast het cirkel diagram om in te zoomen op de apparaten lijst.
1. Met deze actie gaat u naar een tijdelijk knoop punt onder **apparaten** waar u de apparaten kunt zien waarvoor de update is vereist. U kunt ook acties uitvoeren voor het knoop punt, zoals het maken van een nieuwe verzameling in de lijst.

## <a name="servicing-plan-workflow"></a>Werkstroom voor onderhoudsplannen

Windows 10-onderhouds plannen in Configuration Manager zijn veel hetzelfde als regels voor automatische implementatie voor software-updates. U maakt een onderhouds plan met de volgende criteria die door Configuration Manager worden geëvalueerd:

- **De classificatie Upgrades**: alleen de updates met de classificatie **Upgrades** worden geëvalueerd.

- **Gereedheidsstatus**: de gereedheidsstatus die is gedefinieerd in het onderhoudsplan wordt vergeleken met de gereedheidsstatus voor de upgrade. De metagegevens voor de upgrade worden opgehaald wanneer het serviceaansluitpunt controleert op updates.

- **Uitsteltermijn**: het aantal dagen dat u in het onderhoudsplan opgeeft voor **Het aantal dagen dat u wilt wachten met het implementeren van een nieuwe upgrade nadat Microsoft die beschikbaar heeft gesteld**. Als de huidige datum na de release datum plus het geconfigureerde aantal dagen valt, wordt Configuration Manager geëvalueerd of een upgrade in de implementatie moet worden meegenomen.

  Wanneer een upgrade voldoet aan de criteria, voegt het onderhoudsplan de upgrade toe aan het implementatiepakket, distribueert dit het pakket naar de distributiepunten en implementeert het de upgrade voor de verzameling op basis van de instellingen die u in het onderhoudsplan configureert. U kunt de implementaties controleren in de tegel Controle van onderhoudsplannen in het Windows 10-onderhoudsdashboard. Zie [software-updates bewaken](../../sum/deploy-use/monitor-software-updates.md)voor meer informatie.

> [!NOTE]
> **Windows 10, versie 1903 en hoger** is toegevoegd aan Microsoft Update als een eigen product in plaats van dat ze deel uitmaken van het **Windows 10** -product zoals eerdere versies. Als gevolg van deze wijziging hebt u een aantal hand matige stappen uitgevoerd om ervoor te zorgen dat uw clients deze updates zien. We hebben geholpen het aantal hand matige stappen te verminderen dat u moet ondernemen voor het nieuwe product in Configuration Manager versie 1906. Zie [producten configureren voor versies van Windows 10](../../sum/get-started/configure-classifications-and-products.md#windows-10-version-1903-and-later)voor meer informatie.<!--4682946-->

## <a name="windows-10-servicing-plan"></a><a name="BKMK_ServicingPlan"></a> Windows 10-onderhoudsplan

Wanneer u het semi-Annual-kanaal van Windows 10 implementeert, kunt u een of meer onderhouds plannen maken om de implementatie ringen in uw omgeving te definiëren en deze vervolgens te controleren in het Windows 10-onderhouds dashboard. Voor onderhoudsplannen wordt uitsluitend gebruikgemaakt van de software-updateclassificatie **Upgrades** , en niet van de cumulatieve updates voor Windows 10. Voor die updates moet u nog steeds implementeren met behulp van de werk stroom voor software-updates. Het gebruik voor de eindgebruiker bij een onderhoudsplan is hetzelfde als bij de software-updates, waaronder de instellingen die u in het onderhoudsplan configureert.  

> [!NOTE]
> U kunt een takenreeks gebruiken om een upgrade voor elk Windows 10-build te implementeren, maar het vereist meer handmatig werk. U moet de bijgewerkte bronbestanden importeren als een upgradepakket voor besturingssystemen en vervolgens de takenreeks maken en implementeren voor de betreffende verzameling computers. Een takenreeks bevat echter aanvullende aangepaste opties, zoals de acties voorafgaand aan de implementatie en de acties na afloop van de implementatie.

U kunt een basisonderhoudsplan maken in het Windows 10 -onderhoudsdashboard. Nadat u de naam hebt opgegeven, wordt de verzameling (alleen de tien belangrijkste verzamelingen op grootte, kleinste eerst), implementatie pakket (alleen de tien meest recent gewijzigde pakketten worden weer gegeven) en de gereedheids status Configuration Manager het onderhouds plan gemaakt met de standaard waarden voor de overige instellingen. U kunt ook de wizard Onderhoudsplan maken starten om alle instellingen te configureren. U kunt aan de hand van de volgende procedure een onderhoudsplan maken met de wizard Onderhoudsplan maken.  

> [!NOTE]  
> U kunt het gedrag voor implementaties met een hoog risico beheren. Een implementatie met een hoog risico is een implementatie die automatisch wordt geïnstalleerd en de potentie heeft om ongewenste resultaten te veroorzaken. Een takenreeks met het doel **Vereist** en waarmee Windows 10 wordt geïmplementeerd, wordt beschouwd als een implementatie met een hoog risico. Zie [instellingen voor het beheren van implementaties met een hoog risico](../../core/servers/manage/settings-to-manage-high-risk-deployments.md)voor meer informatie.

### <a name="to-create-a-windows-10-servicing-plan"></a>Een Windows 10-onderhoudsplan maken

1. Klik in de Configuration Manager-console op **Softwarebibliotheek**.

1. Vouw in de werkruimte Softwarebibliotheek **Onderhoud voor Windows 10**uit en klik vervolgens op **Onderhoudsplannen**.

1. Klik op het tabblad **Start** in de groep **Maken** op **Onderhoudsplan maken**. De wizard Onderhoudsplan maken wordt geopend.

1. Configureer op de pagina **Algemeen** de volgende instellingen:

    - **Naam**: geef de naam op voor het onderhoudsplan. De naam moet uniek zijn, het doel van de regel beschrijven en deze identificeren van anderen in de Configuration Manager-site.

    - **Beschrijving**: geef een beschrijving op voor het onderhoudsplan. De beschrijving moet een overzicht bieden van het onderhouds plan en eventuele andere relevante informatie waarmee het plan kan worden geïdentificeerd en onderscheiden in de Configuration Manager-site. Het beschrijvingsveld is optioneel en kent een limiet van 256 tekens. Het veld is standaard leeg.

1. Geef op de pagina onderhouds plan de **doel verzameling**op. Leden van de verzameling ontvangen de Windows 10-updates die in het onderhoudsplan zijn gedefinieerd.

    - Wanneer u een implementatie met een hoog risico implementeert, zoals een onderhouds plan, worden in het venster **verzameling selecteren** alleen de aangepaste verzamelingen weer gegeven die voldoen aan de verificatie-instellingen voor de implementatie die zijn geconfigureerd in de eigenschappen van de site.

    - Implementaties met een hoog risico zijn altijd beperkt tot aangepaste verzamelingen, verzameling die uzelf maakt en de ingebouwde verzameling **Onbekende computers** . Wanneer u een implementatie met een hoog risico maakt, kunt u geen ingebouwde verzameling selecteren, zoals **alle systemen**. Schakel het selectie vakje **verzamelingen verbergen met een aantal leden groter dan de minimale configuratie van de site** uit om alle aangepaste verzamelingen weer te geven die minder clients bevatten dan de geconfigureerde maximum grootte. Zie [instellingen voor het beheren van implementaties met een hoog risico](../../core/servers/manage/settings-to-manage-high-risk-deployments.md)voor meer informatie.

    - De instellingen voor het verifiëren van de implementatie zijn gebaseerd op het huidige lidmaatschap van de verzameling. Nadat u het onderhouds plan hebt geïmplementeerd, wordt het lidmaatschap van de verzameling niet opnieuw geëvalueerd voor de implementatie-instellingen met een hoog risico.

      - Stel bijvoorbeeld dat u de **standaard grootte** instelt op 100 en de **maximale grootte** op 1000. Wanneer u een implementatie met een hoog risico maakt, worden in het venster **verzameling selecteren** alleen verzamelingen weer gegeven die minder dan 100 clients bevatten. Als u het selectie vakje **verzamelingen verbergen met een aantal leden dat groter is dan de minimale configuratie-instelling van de site** wist, worden in het venster verzamelingen weer gegeven die minder dan 1000 clients bevatten.  
      Wanneer u een verzameling met een siterol selecteert, geldt de volgende criteria:
        - Als de verzameling een site systeem server bevat en de verificatie-instellingen voor de implementatie die u configureert voor het blok keren van verzamelingen met site systeem servers, treedt er een fout op en kunt u niet door gaan.
        - Als de verzameling een sitesysteemserver bevat en u in de instellingen voor het verifiëren van de implementatie opgeeft dat u moet worden gewaarschuwd als verzamelingen sitesysteemservers bevatten, de verzameling de standaardgrootte overschrijdt of als de verzameling een server bevat, wordt er in de wizard Software implementeren een waarschuwing voor een hoog risico weergegeven. U moet akkoord gaan met het maken van een implementatie met een hoog risico en er wordt een controlestatusbericht gegenereerd.

1. Configureer op de pagina Implementatiering de volgende instellingen:

   - **Geef de Windows-gereedheids status op waarop dit onderhouds plan van toepassing moet zijn**: Selecteer een van de volgende opties:

      - **Semi-Annual-kanaal (targeted)**: in dit onderhouds model zijn onderdelen updates beschikbaar zodra micro soft deze uitbrengt.

      - **Semi-Annual-kanaal**: dit onderhouds kanaal wordt doorgaans gebruikt voor een brede implementatie. Windows 10-clients in het semi-Annual-kanaal ontvangen dezelfde build van Windows 10 als deze apparaten in het doel kanaal, net op een later tijdstip.

        Zie [onderhouds kanalen](/windows/deployment/update/waas-overview#servicing-channels)voor meer informatie over onderhouds kanalen en welke opties voor u het meest geschikt zijn.

   - Hoeveel **dagen nadat micro soft een nieuwe upgrade heeft gepubliceerd, wilt u wachten voordat u deze implementeert in uw omgeving**: als de huidige datum na de release datum plus het aantal dagen dat u configureert voor deze instelling, wordt door Configuration Manager geëvalueerd of een upgrade in de implementatie moet worden opgenomen.

1. Configureer op de pagina upgrades de zoek criteria om de upgrades te filteren die worden toegevoegd aan het service plan. Alleen upgrades die aan de opgegeven criteria voldoen, worden toegevoegd aan de gekoppelde implementatie. De volgende eigenschappen filters zijn beschikbaar: <!--3098809, 3113836, 3204570 -->

   - **Architectuur** (vanaf versie 1810)
   - **Taal**
   - **Product categorie** (vanaf versie 1810)
   - **Vereist**
      > [!IMPORTANT]
      > U wordt aangeraden als onderdeel van uw zoek criteria het **vereiste** veld in te stellen met de waarde **>= 1**. Met deze criteria zorgt u ervoor dat alleen de toepasselijke updates worden toegevoegd aan het service plan.
   - **Vervangen** (vanaf versie 1810)
   - **Titel**

    Klik op **Voorbeeld** om de upgrades weer te geven die voldoen aan de opgegeven criteria.

1. Configureer de volgende instellingen op de pagina Implementatieplanning:

   - **Evaluatie van planning**: Geef op of Configuration Manager de beschik bare tijd en deadline van de installatie evalueert met behulp van UTC of de lokale tijd van de computer waarop de Configuration Manager-console wordt uitgevoerd.

       > [!NOTE]
       > Wanneer u lokale tijd selecteert en vervolgens **zo spoedig mogelijk** selecteert voor de tijd waarop de **software beschikbaar** is of de **installatie deadline**, wordt de huidige tijd op de computer waarop de Configuration Manager-console wordt uitgevoerd, gebruikt om te evalueren wanneer er updates beschikbaar zijn of wanneer ze op een client worden geïnstalleerd. Als de client zich in een andere tijdzone bevindt, worden deze acties uitgevoerd wanneer de tijd van de client de evaluatietijd heeft bereikt.

   - **Tijd waarop de software beschikbaar is**: selecteer een van de volgende instellingen om op te geven wanneer de software-updates beschikbaar worden gemaakt voor clients:

        - **Zo spoedig mogelijk**: selecteer deze instelling om de software-updates in de implementatie zo spoedig mogelijk beschikbaar te maken voor clientcomputers. Wanneer u de implementatie maakt terwijl deze instelling is geselecteerd, wordt het client beleid door Configuration Manager bijgewerkt. Vervolgens wordt bij de volgende polling-cyclus voor client beleid op de hoogte gebracht van de implementatie en kunnen de updates worden opgehaald die beschikbaar zijn voor installatie.

        - **Specifiek tijdstip**: selecteer deze instelling om de software-updates in de implementatie op een specifieke datum en tijd beschikbaar te maken voor de clientcomputers. Wanneer u de implementatie maakt terwijl deze instelling is ingeschakeld, wordt het client beleid door Configuration Manager bijgewerkt. Clients detecteren de implementatie vervolgens gedurende de volgende pollingcyclus van het clientbeleid. De software-updates in de implementatie zijn echter pas na de geconfigureerde datum en tijd beschikbaar voor installatie.

   - **Installatie deadline**: Selecteer een van de volgende instellingen om de installatie deadline op te geven voor de software-updates in de implementatie:

        - **Zo spoedig mogelijk**: selecteer deze instelling als u wilt dat de software-updates in de implementatie zo spoedig mogelijk automatisch worden geïnstalleerd.

        - **Specifiek tijdstip**: selecteer deze instelling als u wilt dat de software-updates in de implementatie automatisch worden geïnstalleerd op een specifieke datum en tijd. Configuration Manager bepaalt de deadline voor het installeren van software-updates door het geconfigureerde **specifieke tijds** interval toe te voegen aan de **beschik bare tijd**van de software.

           > [!NOTE]
           > Het daadwerkelijke tijdstip van de installatiedeadline is het weergegeven deadlinetijdstip plus een willekeurige hoeveelheid die maximaal twee uur is. Hierdoor worden de mogelijk gevolgen voorkomen wanneer de updates in de implementatie gelijktijdig op alle clientcomputers in de doelverzameling zouden worden geïnstalleerd.
           >
           > U kunt de **Computeragent** -clientinstelling **Willekeurig toepassen van deadline uitschakelen** configureren om de willekeurige installaties voor de vereiste updates uit te schakelen. Zie [Computeragent](../../core/clients/deploy/about-client-settings.md#computer-agent)voor meer informatie.

        - **Het afdwingen van deze implementatie op basis van gebruikers voorkeuren uitstellen tot de respijt periode die op de client is gedefinieerd**: Selecteer deze optie om te voldoen aan de [ **respijt periode voor afdwingen na de client instelling voor de deadline van de implementatie (uren)** ](../../core/clients/deploy/about-client-settings.md#grace-period-for-enforcement-after-deployment-deadline-hours).

1. Configureer de volgende instellingen op de pagina Gebruikerservaring:  

    - **Meldingen voor gebruikers**: geef op of meldingen van de updates in Software Center op de clientcomputer moeten worden weergeven op de geconfigureerde **Tijd waarop de software beschikbaar is** en of meldingen voor gebruikers moeten worden weergegeven op de clientcomputers.

    - **Deadlinegedrag**: geef het gedrag op dat moet worden vertoond als de deadline voor de implementatie van de update wordt bereikt. Geef op of de updates in de implementatie moeten worden geïnstalleerd. Geef ook op of het systeem na het installeren van de updates opnieuw moet worden opgestart, ongeacht het geconfigureerde onderhoudsvenster. Zie [onderhouds Vensters gebruiken](../../core/clients/manage/collections/use-maintenance-windows.md)voor meer informatie over onderhouds Vensters.  

    - **Gedrag voor het opnieuw opstarten van apparaten**: geef op of het opnieuw opstarten van servers en werkstations na de installatie van de updates moet worden onderdrukt en of het opnieuw opstarten is vereist om de installatie te voltooien.

    - **Verwerking van schrijffilters voor Windows Embedded-apparaten**: wanneer u updates implementeert voor Windows Embedded-apparaten waarvoor schrijffilters zijn ingeschakeld, kunt u aangeven dat u de update op een tijdelijke overlay wilt installeren en de wijzigingen later aanbrengt of dat u de wijzigingen aanbrengt bij het bereiken van de installatiedeadline of tijdens een onderhoudsvenster. Wanneer u wijzigingen doorvoert tegen de installatiedeadline of tijdens een onderhoudsvenster, moet er opnieuw worden opgestart, zodat de wijzigingen behouden blijven op het apparaat.
        - Wanneer u een update implementeert op een Windows Embedded-apparaat, moet u nagaan of het apparaat lid is van een verzameling met een geconfigureerd onderhoudsvenster.

    - **Gedrag van nieuwe evaluatie van software-updates na opnieuw opstarten**: als u de evaluatie cyclus van een nieuwe update-implementatie wilt afdwingen, selecteert u de optie **als een update in deze implementatie vereist is dat het systeem opnieuw wordt opgestart, voert u de evaluatie cyclus voor de implementatie van updates uit na opnieuw opstarten**.

1. Selecteer op de pagina implementatie pakket een bestaand implementatie pakket, geen implementatie pakket of configureer de volgende instellingen voor het maken van een nieuw implementatie pakket:

    1. **Naam**: geef de naam op van het implementatiepakket. Deze naam moet uniek zijn en beschrijft de pakket inhoud. Het is beperkt tot 50 tekens.

    1. **Beschrijving**: geef een beschrijving op die informatie biedt over het implementatiepakket. De beschrijving mag niet langer zijn dan 127 tekens.

    1. **Pakketbron**: hiermee geeft u de locatie op van de bronbestanden van de software-update. Typ een netwerkpad voor de bron locatie, bijvoorbeeld ** \\\Server\\share\\naam pad**of klik op **Bladeren** om de netwerk locatie te zoeken. Maak de gedeelde map voor de bron bestanden van het implementatie pakket voordat u doorgaat naar de volgende pagina.
        - De bronlocatie van het installatiepakket die u opgeeft, mag niet door een ander software-installatiepakket worden gebruikt.
        - Het computeraccount van de SMS-provider en de gebruiker die de wizard uitvoert voor het downloaden van de software-updates, moeten over NTFS-machtigingen voor **schrijven** op de downloadlocatie beschikken. U moet de toegang tot de download locatie zorgvuldig beperken om het risico te beperken dat kwaadwillende personen knoeien met de bron bestanden van de software-update.
        - U kunt de pakket bron locatie wijzigen in de eigenschappen van het implementatie pakket nadat Configuration Manager het implementatie pakket hebt gemaakt. Als u dit doet, moet u echter eerst de inhoud van de oorspronkelijke pakketbron kopiëren naar de nieuwe pakketbronlocatie.

    1. **Prioriteit voor verzenden**: geef de prioriteit op voor verzenden van het implementatiepakket. Configuration Manager maakt gebruik van de prioriteit voor verzenden voor het implementatie pakket wanneer het pakket naar distributie punten wordt verzonden. Implementatie pakketten worden in volg orde van prioriteit verzonden: hoog, gemiddeld of laag. Pakketten met een identieke prioriteit worden verzonden in de volgorde waarin deze zijn gemaakt. Als er geen achterstand is, wordt het pakket onmiddellijk verwerkt, ongeacht de prioriteit.

    1. **Binary Differential Replication inschakelen**: Schakel deze optie in als u binary Differential Replication wilt gebruiken.

1. Geef op de pagina distributie punten de distributie punten of distributiepunten groepen op die als host dienen voor de update bestanden. Zie [Configure a Distribution Point (een distributie punt configureren](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs)) voor meer informatie over distributie punten.

    > [!NOTE]
    > Deze pagina is alleen beschikbaar wanneer u een nieuw implementatiepakket voor software-updates maakt.  

1. Geef op de pagina Downloadlocatie op of de updatebestanden moeten worden gedownload vanaf internet of vanaf uw lokale netwerk. Configureer de volgende instellingen:

    - **Software-updates downloaden van internet**: selecteer deze instelling om de updates vanaf een opgegeven locatie op internet te downloaden. Deze instelling is standaard ingeschakeld.

    - **Software-updates downloaden van een locatie in het lokale netwerk**: selecteer deze instelling als u de updates vanaf een lokale map of gedeelde map wilt downloaden. Deze instelling is nuttig wanneer de computer waarop de wizard wordt uitgevoerd, geen toegang tot internet heeft. Computers met internettoegang kunnen de updates in eerste instantie downloaden en deze opslaan op een locatie in het lokale netwerk die toegankelijk is vanaf de computer waarop de wizard wordt uitgevoerd.

1. Selecteer op de pagina Taal selecteren de talen waarvoor de geselecteerde updates worden gedownload. De updates worden alleen gedownload als deze beschikbaar zijn in de geselecteerde talen. Updates die niet taalspecifiek zijn, worden altijd gedownload. De wizard selecteert standaard de talen die u hebt geconfigureerd in de eigenschappen van het software-update punt. Er moet ten minste één taal worden geselecteerd voordat u doorgaat naar de volgende pagina. Wanneer u alleen talen selecteert die niet door een update worden ondersteund, mislukt het downloaden van de update.

1. Controleer op de overzichtspagina de instellingen en klik vervolgens op **Volgende** om het onderhoudsplan te maken.  

Nadat u de wizard hebt voltooid, wordt het onderhouds plan uitgevoerd. Het voegt de updates toe die voldoen aan de opgegeven criteria voor een software-update groep, downloadt de updates naar de inhouds bibliotheek op de site server, distribueert de updates naar de geconfigureerde distributie punten en implementeert vervolgens de software-update groep voor clients in de doel verzameling.

## <a name="modify-a-servicing-plan"></a><a name="BKMK_ModifyServicingPlan"></a> Een onderhoudsplan wijzigen

Nadat u een Basic-onderhouds plan hebt gemaakt op basis van het Windows 10-onderhouds dashboard of als u de instellingen voor een bestaand onderhouds plan wilt wijzigen, gaat u naar de eigenschappen voor het onderhouds plan.

> [!NOTE]
> U kunt in de eigenschappen voor het onderhouds plan instellingen configureren die niet beschikbaar zijn in de wizard wanneer u het onderhouds plan maakt. De wizard gebruikt de standaard instellingen voor de volgende instellingen: Download instellingen, implementatie-instellingen en waarschuwingen.  

Gebruik de volgende procedure om de eigenschappen van een onderhoudsplan te wijzigen. 

### <a name="to-modify-the-properties-of-a-servicing-plan"></a>De eigenschappen van een onderhoudsplan wijzigen

1. Klik in de Configuration Manager-console op **Softwarebibliotheek**.

1. In de werk ruimte software bibliotheek vouwt u **Windows 10-onderhoud**uit, klikt u op **onderhouds plannen**en selecteert u vervolgens het onderhouds plan dat u wilt wijzigen.

1. Klik op het tabblad **Start** op **Eigenschappen** om de eigenschappen van het geselecteerde onderhoudsplan weer te geven.

    De volgende instellingen zijn beschikbaar in de eigenschappen van het onderhouds plan die niet in de wizard zijn geconfigureerd:

    **Implementatie-instellingen**: Configureer op het tabblad implementatie-instellingen de volgende instellingen:

    - **Wake-on-LAN gebruiken om clients te laten ontwaken voor vereiste implementaties**: geef op of Wake-on-LAN op de deadline moet worden ingeschakeld om ontwaakpakketten te verzenden naar computers waarvoor een of meer software-updates in de implementatie zijn vereist. Computers die zich in de slaap stand bevinden tijdens de deadline van de installatie, worden geactiveerd zodat de installatie van de software-update kan worden gestart. Clients die zich in de slaap stand bevinden en geen software-updates nodig hebben in de implementatie, worden niet gestart. Deze instelling is standaard niet ingeschakeld.

        > [!WARNING]
        > Voordat u deze optie kunt gebruiken, moeten computers en netwerken zijn geconfigureerd voor Wake On LAN.

    - **Detailniveau**: geef het detailniveau op voor de statusberichten die worden gerapporteerd door clientcomputers.

    **Instellingen voor downloaden**: Configureer de volgende instellingen op het tabblad Download instellingen:

    - Geef op of de client de software-updates moet downloaden en installeren wanneer een client is verbonden met een langzaam netwerk of gebruikmaakt van een terugval locatie voor inhoud.

    - Geef op of de client de software-updates moet downloaden en installeren vanaf een terugval distributiepunt wanneer de inhoud voor de software-updates niet beschikbaar is op een voorkeurs distributiepunt.

    - **Clients toestaan inhoud te delen met andere clients in hetzelfde subnet**: hier kunt u aangeven of het gebruik van BranchCache moet worden ingeschakeld voor het downloaden van inhoud. Zie [basis concepten voor inhouds beheer](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache)voor meer informatie over BranchCache.

    - Geef op of clients software-updates moeten downloaden van Microsoft Update als software-updates niet beschikbaar zijn op distributie punten.
        > [!IMPORTANT]
        > Gebruik deze instelling niet voor Windows 10-onderhouds updates. Configuration Manager (ten minste via versie 1610) kan de Windows 10-onderhouds updates niet downloaden van Microsoft Update.

    - Geef op of clients mogen downloaden na een installatiedeadline wanneer deze internetverbindingen met een datalimiet gebruiken. Internetproviders brengen soms de hoeveelheid gegevens die u verzendt en ontvangt in rekening wanneer u gebruikmaakt van een internetverbinding naar gebruik.

    **Waarschuwingen**: Configureer op het tabblad waarschuwingen hoe Configuration Manager en System Center Operations Manager waarschuwingen voor deze implementatie worden gegenereerd.
    - U kunt recente waarschuwingen met betrekking tot software-updates weergeven in het knooppunt **Software-updates** in de werkruimte **Softwarebibliotheek**.

## <a name="next-steps"></a>Volgende stappen

Zie [de grond beginselen van Configuration Manager als een service en Windows als een service](../../core/understand/configuration-manager-and-windows-as-service.md)voor meer informatie.
