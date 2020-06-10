---
title: Updates binnen de console
titleSuffix: Configuration Manager
description: Updates voor Configuration Manager installeren vanuit de micro soft-Cloud
ms.date: 06/02/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a0d7f36c921f782c0baad740d8e643f54cee0309
ms.sourcegitcommit: 5e339c07001e911cf75ef922e6c66a7efdeab6f1
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/10/2020
ms.locfileid: "84637666"
---
# <a name="install-in-console-updates-for-configuration-manager"></a>Updates in de console installeren voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager synchroniseert met de micro soft-Cloud service om updates op te halen. Installeer deze updates vervolgens vanuit de Configuration Manager-console.

## <a name="get-available-updates"></a>Beschikbare updates downloaden

De site downloadt alleen updates die van toepassing zijn op uw infra structuur en versie. Deze synchronisatie kan automatisch of hand matig zijn, afhankelijk van hoe u het service verbindings punt voor uw hiërarchie configureert:

- In **onlinemodus**maakt het serviceverbindingspunt automatisch verbinding met de Microsoft-cloudservice en worden toepasselijke updates gedownload.  

    Configuration Manager controleert standaard elke 24 uur op nieuwe updates. Hand matig controleren op updates in de Configuration Manager-console. Ga naar de werk ruimte **beheer** , selecteer het knoop punt **updates en onderhoud** en kies **controleren op updates** in het lint.  

- In de **offline modus**maakt het service verbindings punt geen verbinding met de micro soft-Cloud service. [Gebruik het hulp programma voor service verbindingen](use-the-service-connection-tool.md)om beschik bare updates te downloaden en vervolgens te importeren.  

> [!NOTE]  
> Indien nodig kunt u out-of-band-oplossingen importeren in uw-console. Gebruik hiervoor het [hulp programma Registratie bijwerken](use-the-update-registration-tool-to-import-hotfixes.md). Deze out-of-band-oplossingen vormen een aanvulling op de updates die u ontvangt wanneer u synchroniseert met de micro soft-Cloud service.  

Nadat de updates zijn gesynchroniseerd, kunt u deze bekijken in de Configuration Manager-console. Ga naar de werk ruimte **beheer** en selecteer het knoop punt **updates en onderhoud** .  

- Updates die u niet hebt geïnstalleerd, worden weer gegeven als **beschikbaar**.  

- De updates die u hebt geïnstalleerd, worden weer gegeven als **geïnstalleerd**. Alleen de meest recent geïnstalleerde update wordt weer gegeven. Als u eerder geïnstalleerde updates wilt weer geven, selecteert u **geschiedenis** op het lint.  

Voordat u het service aansluitpunt configureert, begrijpt en plant u het aanvullende gebruik. De volgende gebruiks mogelijkheden zijn mogelijk van invloed op hoe u deze site systeemrol configureert:  

- De site maakt gebruik van het service verbindings punt voor het uploaden van gebruiks gegevens over uw site. Deze informatie helpt de Microsoft-cloudservice bij het identificeren van de updates die beschikbaar zijn voor de huidige versie van uw infrastructuur. Zie [diagnostiek en gebruiks gegevens](../../plan-design/diagnostics/diagnostics-and-usage-data.md)voor meer informatie.  

Zie de volgende stroom diagrammen voor meer informatie over wat er gebeurt wanneer er updates worden gedownload:  

- [Stroomdiagram: updates downloaden](download-updates-flowchart.md)  

- [Stroomdiagram: updatereplicatie](update-replication-flowchart.md)  

## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Machtigingen toewijzen voor het weer geven en beheren van updates en functies

Als u updates wilt weer geven in de-console, moet een gebruiker een op rollen gebaseerde beheer beveiligingsrol hebben die de **update pakketten**voor beveiligings klassen bevat. Deze klasse verleent toegang voor het weer geven en beheren van updates in de Configuration Manager-console.

### <a name="about-the-update-packages-class"></a>Over de klasse update pakketten

De klasse **update pakketten** (SMS_CM_Updatepackages) is standaard onderdeel van de volgende ingebouwde beveiligings rollen met de vermelde machtigingen:  

- **Volledige beheerder** met de machtigingen **Wijzigen** en **Lezen** :  

  - Een gebruiker met deze beveiligingsrol en toegang tot het beveiligings bereik **alle** kan updates weer geven en installeren. De gebruiker kan ook functies inschakelen tijdens de installatie en afzonderlijke functies inschakelen nadat de site is bijgewerkt.  

  - Een gebruiker met deze beveiligingsrol en toegang tot het beveiligings bereik **standaard** kan updates weer geven en installeren. De gebruiker kan ook functies inschakelen tijdens de installatie en de functies weer geven nadat de site is bijgewerkt. Maar deze gebruiker kan de functies niet inschakelen nadat de site is bijgewerkt.  

- **Alleen-lezenanalist** met **lees** machtigingen:  

  - Een gebruiker met deze beveiligingsrol en toegang tot het **standaard** bereik kan updates weer geven, maar niet installeren. Deze gebruiker kan ook functies weer geven nadat de site is bijgewerkt, maar deze kan niet worden ingeschakeld.  

### <a name="permissions-required-for-updates-and-servicing"></a>Machtigingen die vereist zijn voor updates en onderhoud

- Gebruik een account waaraan u een beveiligingsrol kunt toewijzen die de klasse **update pakketten** bevat met de machtigingen **wijzigen** en **lezen** .  

- Wijs het account toe aan het **standaard** bereik.  

### <a name="permissions-to-only-view-updates"></a>Machtigingen voor het weer geven van updates

- Gebruik een account waaraan u een beveiligingsrol kunt toewijzen die de klasse **update pakketten** bevat met alleen de machtiging **lezen** .  

- Wijs het account toe aan het **standaard** bereik.  

### <a name="permissions-required-to-enable-features-after-the-site-updates"></a>Benodigde machtigingen voor het inschakelen van functies na site-updates

- Gebruik een account waaraan u een beveiligingsrol kunt toewijzen die de klasse **update pakketten** bevat met de machtigingen **wijzigen** en **lezen** .  

- Wijs het account toe aan het bereik **Alles** .  

## <a name="before-you-install-an-in-console-update"></a><a name="bkmk_beforeinstall"></a>Voordat u een update in de console installeert  

Bekijk de volgende stappen voordat u een update installeert in de Configuration Manager-console.  

### <a name="step-1-review-the-update-checklist"></a><a name="bkmk_step1"></a>Stap 1: de controle lijst voor updates controleren  

Bekijk de toepasselijke controle lijst voor updates voor acties die moeten worden uitgevoerd voordat u de update start:

- [Controlelijst voor het installeren van update 2002](checklist-for-installing-update-2002.md)

- [Controlelijst voor het installeren van update 1910](checklist-for-installing-update-1910.md)  

- [Controlelijst voor het installeren van update 1906](checklist-for-installing-update-1906.md)  

- [Controlelijst voor het installeren van update 1902](checklist-for-installing-update-1902.md)

### <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a><a name="bkmk_step2"></a>Stap 2: de prerequisite Checker uitvoeren voordat u een update installeert  

Het wordt aangeraden de controle op vereisten voor een update uit te voeren voordat u deze update installeert. Als u de prerequisite checker uitvoert voordat u een update installeert:  

- De site repliceert update bestanden naar andere sites voordat de update wordt geïnstalleerd.  

- Wanneer u ervoor kiest om de update te installeren, wordt de controle op vereisten automatisch opnieuw uitgevoerd.  

> [!NOTE]  
> Wanneer u een controle op vereisten start en vervolgens de status bekijkt, lijkt de **installatie** fase actief te zijn. De-site installeert echter niet echt de update. Als u de controle op vereisten wilt uitvoeren, haalt het update proces het pakket op uit de inhouds bibliotheek. Vervolgens wordt het pakket in een tijdelijke map geplaatst waarin het toegang heeft tot de huidige vereisten controles. Wanneer u een update installeert, wordt hetzelfde proces uitgevoerd. Dit is de reden waarom de installatie fase wordt weer gegeven als **in behandeling**. Alleen de stap *Update pakket uitpakken* wordt weer gegeven in de categorie installatie.  

Wanneer u de update later installeert, kunt u de update configureren om de waarschuwingen voor vereisten controleren te negeren.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>De controle van vereisten uitvoeren voordat u een update installeert  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** en selecteer het knoop punt **updates en onderhoud** .  

2. Selecteer het update pakket waarvoor u de controle op vereisten wilt uitvoeren.  

3. Selecteer **controle van vereisten uitvoeren** op het lint.  

    Wanneer u de controle op vereisten uitvoert, wordt inhoud voor de update gerepliceerd naar onderliggende sites. Bekijk de **distmgr. log** op de site server om te bevestigen dat de inhoud is gerepliceerd.  

4. De resultaten van de controle op vereisten weer geven:  

    1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** .  

    2. Selecteer het knoop punt **updates en onderhoud status** en zoek de vereiste status.  

    3. Zie **ConfigMgrPrereq. log** op de site server voor meer informatie.  

## <a name="install-in-console-updates"></a><a name="bkmk_install"></a>Updates in de console installeren  

Wanneer u klaar bent om updates te installeren vanuit de Configuration Manager console, begint u met de site op het hoogste niveau van uw hiërarchie. Deze site is de centrale beheer site of een zelfstandige primaire site.  

Installeer de update buiten kantoor uren voor elke site om het effect op bedrijfs bewerkingen te minimaliseren. De installatie van de update bevat mogelijk acties zoals het opnieuw installeren van site onderdelen en site systeem rollen.  

- Bij onderliggende primaire sites wordt de update automatisch gestart nadat de installatie van de update is voltooid op de centrale beheer site. Dit proces is standaard en wordt aanbevolen. Als u wilt bepalen wanneer updates worden geïnstalleerd op een primaire site, gebruikt u [service Windows voor site servers](service-windows.md).  

- Nadat de update van de primaire bovenliggende site is voltooid, moet u de secundaire sites hand matig bijwerken vanuit de Configuration Manager-console. Het automatisch bijwerken van secundaire site servers wordt niet ondersteund.  

- Wanneer u een Configuration Manager-console gebruikt nadat de site is bijgewerkt, wordt u gevraagd de console bij te werken.  

- Nadat de installatie van een update door de site server is voltooid, worden automatisch alle toepasselijke site systeem rollen bijgewerkt. Alle distributie punten worden echter niet opnieuw geïnstalleerd en offline gaan om tegelijkertijd te worden bijgewerkt. In plaats daarvan gebruikt de site server de inhouds distributie-instellingen van de site om de update te distribueren naar een subset van distributie punten tegelijk. Het resultaat is dat slechts enkele distributie punten offline gaan om de update te installeren. Distributie punten die niet zijn begonnen met het bijwerken of die de update hebben voltooid, blijven online en kunnen inhoud aan clients leveren.

### <a name="overview-of-in-console-update-installation"></a><a name="bkmk_overview"></a>Overzicht van de installatie van de update in de console  

#### <a name="1-when-the-update-installation-starts"></a>1. Wanneer de installatie van een update wordt gestart

U krijgt de wizard updates te zien waarin een lijst wordt weer gegeven met de product gebieden waarop de update van toepassing is.  

- Configureer op de pagina **Algemeen** van de wizard **vereiste waarschuwingen** als dat nodig is:  

  - De installatie van de update wordt altijd gestopt als een fout optreedt in de vereisten. Corrigeer fouten voordat u de installatie van de update opnieuw kunt uitvoeren. Zie [de installatie van een mislukte update opnieuw uitvoeren](#bkmk_retry)voor meer informatie.  

  - Waarschuwingen voor vereisten kunnen ook de installatie van updates stoppen. Corrigeer waarschuwingen voordat u de installatie van de update opnieuw installeert. Zie [de installatie van een mislukte update opnieuw uitvoeren](#bkmk_retry)voor meer informatie.  

  - **De waarschuwingen voor vereisten controleren negeren en deze update installeren ongeacht ontbrekende vereisten**: Stel een voor waarde in voor de installatie van de update om waarschuwingen over vereisten te negeren. Met deze optie kan de installatie van de update worden voortgezet. Als u deze optie niet selecteert, stopt de installatie van de update wanneer er een waarschuwing wordt aangetroffen door het proces. Gebruik deze optie alleen als u eerder de controle op vereisten hebt uitgevoerd en waarschuwingen met betrekking tot de vereisten voor een site hebt hersteld.  

    In de werk ruimten **beheer** en **bewaking** bevat het knoop punt updates en onderhoud een knop in het lint met de naam **waarschuwingen over vereisten negeren**. Deze knop wordt beschikbaar wanneer een update pakket de installatie niet kan volt ooien vanwege waarschuwingen over vereiste controles. U installeert bijvoorbeeld een update zonder gebruik te maken van de optie om waarschuwingen over vereisten te negeren (vanuit de wizard updates). De installatie van de update stopt met de status waarschuwing voor vereisten, maar zonder fouten. Later selecteert u **waarschuwingen voor vereisten negeren** op het lint. Met deze actie wordt een automatische voortzetting van de installatie van de update geactiveerd, waarmee waarschuwingen voor vereisten worden genegeerd. Wanneer u deze optie gebruikt, wordt de installatie van de update na enkele minuten automatisch voortgezet.  

- Wanneer een update van toepassing is op de Configuration Manager-client, moet u ervoor kiezen om de client update te testen met een beperkte set clients. Zie [Client upgrades testen in een pre-productie verzameling](../../clients/manage/upgrade/test-client-upgrades.md)voor meer informatie.  

#### <a name="2-during-the-update-installation"></a>2. Tijdens de installatie van een update

Als onderdeel van de installatie van de update voert Configuration Manager de volgende acties uit:  

- Alle betrokken onderdelen, zoals site systeem rollen of de Configuration Manager-console, worden opnieuw geïnstalleerd.  

- Hiermee worden updates beheerd voor clients op basis van de selecties die u hebt gemaakt voor de client proef en voor [automatische Client upgrades](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate).  

- Site systeem servers hoeven over het algemeen niet opnieuw te worden opgestart als onderdeel van de update. Als een rol .NET gebruikt en het pakket het vereiste onderdeel bijwerkt, wordt het site systeem mogelijk opnieuw opgestart.  

> [!TIP]  
> Wanneer u Configuration Manager updates installeert, werkt de site ook de CD bij. Meest recente map. Zie de CD voor meer informatie [. Meest recente map](the-cd.latest-folder.md).  

#### <a name="3-monitor-the-progress-of-updates-as-they-install"></a>3. De voortgang van de updates bewaken tijdens de installatie

Gebruik de volgende stappen om de voortgang te controleren:  

- Ga in de Configuration Manager-console naar de werk ruimte **beheer** en selecteer het knoop punt **updates en onderhoud** . Dit knooppunt geeft de installatiestatus weer voor alle updatepakketten.  

- Ga in de Configuration Manager-console naar de werk ruimte **bewaking** en selecteer het knoop punt **updates en onderhoud status** . Dit knoop punt geeft de installatie status weer van alleen het huidige update pakket dat door de site wordt geïnstalleerd.  

    De installatie van de update is onderverdeeld in verschillende fasen voor een eenvoudiger bewaking. Voor elk van de volgende fasen bevat het logboek bestand dat u wilt weer geven extra informatie over de installatie status:  

  - **Downloaden**: deze fase is alleen van toepassing op de site op het hoogste niveau met het service aansluitpunt.

  - **Replicatie**

  - **Vereistencontrole**

  - **Installatie**

  - **Post-installatie**: Zie [taken na de installatie](#post-installation-tasks)voor meer informatie.  

- Bekijk het bestand **CMUpdate. log** in `<ConfigMgr_Installation_Directory>\Logs` op de site server.  

>[!NOTE]
> Vanaf versie 1906 ziet u de status van de taak ConfigMgr- **Data Base bijwerken** tijdens de **installatie** fase.
>
> - Als de data base-upgrade is geblokkeerd, krijgt u de waarschuwing dat deze wordt **uitgevoerd**.
>   - De naam van het programma en de SessionID van SQL die de data base-upgrade blokkeert, worden door cmupdate. log geregistreerd.
> - Wanneer de upgrade van de data base niet meer wordt geblokkeerd, wordt de status opnieuw ingesteld op **actief** of **voltooid**.
>   - Wanneer de data base-upgrade is geblokkeerd, wordt elke vijf minuten een controle uitgevoerd om te zien of deze nog steeds wordt geblokkeerd.

#### <a name="4-when-the-update-installation-completes"></a>4. Wanneer de installatie van een update is voltooid

Nadat de installatie van de update voor de eerste site is voltooid:  

- De update wordt automatisch geïnstalleerd op onderliggende primaire sites. Er is geen verdere actie vereist.  

- Secundaire sites hand matig bijwerken vanuit de Configuration Manager-console. Zie [de installatie van de update op een secundaire site starten](#bkmk_secondary)voor meer informatie.  

- Uw hiërarchie draait in een modus van gemengde versies totdat alle sites in uw hiërarchie zijn bijgewerkt naar de nieuwe versie. Zie [interoperabiliteit tussen verschillende versies](../../plan-design/hierarchy/interoperability-between-different-versions.md)voor meer informatie.  

#### <a name="5-update-configuration-manager-consoles"></a>5. Configuration Manager-consoles bijwerken

Na een update van een centrale beheer site of primaire site moet elke Configuration Manager-console die verbinding maakt met de site ook worden bijgewerkt. U wordt gevraagd een console bij te werken:  

- Wanneer u de console opent  

- Wanneer u naar een nieuw knoop punt in een geopende console gaat  

Werk de console direct bij nadat de site is bijgewerkt.  

Nadat de-console-update is voltooid, controleert u of de versies van de console en site correct zijn. Ga naar **over Configuration Manager** in de linkerbovenhoek van de console.  

> [!Note]  
> De console versie wijkt enigszins af van de versie van de site. De secundaire versie van de console komt overeen met de Configuration Manager Release versie. In Configuration Manager versie 1802 is de eerste site versie bijvoorbeeld 5.0.8634.1000 en is de oorspronkelijke console versie 5. **1802**. 1082,1700. De buildnummers (1082) en revisie (1700) kan veranderen met toekomstige hotfixes.

### <a name="to-start-the-update-installation-at-the-top-level-site"></a><a name="bkmk_toptier"></a>De installatie van de update op de site op het hoogste niveau starten  

Ga op de site op het hoogste niveau van uw hiërarchie naar de werk ruimte **beheer** in de Configuration Manager-console en selecteer het knoop punt **updates en onderhoud** . Selecteer een update met de status **beschikbaar**en kies vervolgens **Update pakket installeren** op het lint.  

### <a name="to-start-the-update-installation-at-a-secondary-site"></a><a name="bkmk_secondary"></a>De installatie van de update op een secundaire site starten  

Nadat de bovenliggende primaire site van een secundaire site is bijgewerkt, werkt u de secundaire site bij vanuit de Configuration Manager-console. Hiervoor gebruikt u de **Wizard Upgrade van secundaire Site**.  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** . Selecteer de secundaire site die u wilt bijwerken en kies vervolgens **bijwerken** in het lint.  

2. Selecteer **Ja** om de update van de secundaire site te starten.  

Als u de installatie van de update op een secundaire site wilt controleren, selecteert u de secundaire site en kiest u **installatie status weer geven** in het lint. Voeg ook de kolom **versie** toe aan het knoop punt sites, zodat u de versie van elke secundaire site kunt bekijken.  

In sommige gevallen wordt de status in de console niet vernieuwd of raadt de update niet aan. Nadat een secundaire site is bijgewerkt, gebruikt u de optie **installatie opnieuw proberen** . Met deze optie wordt de update voor een secundaire site waarop de update is geïnstalleerd, niet opnieuw geinstalleerd, maar wordt de status van de console bijgewerkt.

### <a name="post-installation-tasks"></a>Taken na de installatie

Wanneer een-site een update installeert, zijn er verschillende taken die pas kunnen worden gestart nadat de installatie van de update op de site server is voltooid. Deze lijst bevat de taken na de installatie die essentieel zijn voor site-en hiërarchie bewerkingen. Omdat ze kritiek zijn, worden ze actief gecontroleerd. Aanvullende taken die niet rechtstreeks worden bewaakt, zijn onder andere het opnieuw installeren van site systeem rollen. Als u de status van de kritieke taken na de installatie wilt bekijken, selecteert u de taak **na** de installatie tijdens het controleren van de installatie van de update voor een-site.

Niet alle taken zijn onmiddellijk voltooid. Sommige taken worden pas gestart nadat de installatie van de update is voltooid op elke site. De nieuwe functionaliteit die u mogelijk verwacht, kan worden uitgesteld totdat deze taken zijn voltooid. Het inschakelen van nieuwe functies wordt pas gestart als alle sites de installatie van de update volt ooien, waardoor nieuwe functies mogelijk niet langer zichtbaar zijn.

De taken na de installatie zijn onder andere:

- **SMS_EXECUTIVE-service installeren**

  - Essentiële service die op de site server wordt uitgevoerd.
  - Het opnieuw installeren van deze service moet snel worden voltooid.

- **SMS_DATABASE_NOTIFICATION_MONITOR onderdeel installeren**

  - Kritieke site onderdeel thread van SMS_EXECUTIVE service.
  - Het opnieuw installeren van deze service moet snel worden voltooid.

- **SMS_HIERARCHY_MANAGER onderdeel installeren**

  - Kritiek site onderdeel dat wordt uitgevoerd op de site server.
  - Verantwoordelijk voor het opnieuw installeren van rollen op site systeem servers. Status voor het opnieuw installeren van de afzonderlijke site systeemrol wordt niet weer gegeven.
  - Het opnieuw installeren van deze service moet snel worden voltooid.

    > [!Note]
    > Sommige Configuration Manager site rollen delen het client-Framework. Bijvoorbeeld het beheer punt en het pull-distributie punt. Wanneer deze rollen worden bijgewerkt, wordt de client versie op deze servers op hetzelfde moment bijgewerkt. Zie [clients bijwerken](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md)voor meer informatie.

- **SMS_REPLICATION_CONFIGURATION_MONITOR onderdeel installeren**

  - Kritiek site onderdeel dat wordt uitgevoerd op de site server.
  - Het opnieuw installeren van deze service moet snel worden voltooid.

- **SMS_POLICY_PROVIDER onderdeel installeren**

  - Kritiek site onderdeel dat alleen op primaire sites wordt uitgevoerd.
  - Het opnieuw installeren van deze service moet snel worden voltooid.

- **Replicatie-initialisatie controleren**

  - Deze taak wordt alleen weer gegeven op de centrale beheer site en de onderliggende primaire sites.
  - Afhankelijk van de SMS_REPLICATION_CONFIGURATION_MONITOR.
  - Moet snel worden voltooid.

- **Pakket met Configuration Manager client-preproductie bijwerken**

  - Deze taak wordt zelfs weer gegeven wanneer client-preproductie (ook wel client piloten genoemd) niet is ingeschakeld voor gebruik.
  - Start niet totdat alle sites in de hiërarchie de installatie van de update volt ooien.

- **De map client op de site server wordt bijgewerkt**

  - Deze taak wordt niet weer gegeven als u de-client gebruikt in een preproductie.  
  - Moet snel worden voltooid.

- **Configuration Manager-client pakket bijwerken**

  - Deze taak wordt niet weer gegeven als u de-client gebruikt in een preproductie.  
  - Wordt pas voltooid nadat de update is geïnstalleerd door alle sites.  

- **Functies inschakelen**

  - Deze taak wordt alleen weer gegeven op de site op het hoogste niveau van de hiërarchie.
  - Start niet totdat alle sites in de hiërarchie de installatie van de update volt ooien.
  - Afzonderlijke functies worden niet weer gegeven.

## <a name="retry-installation-of-a-failed-update"></a><a name="bkmk_retry"></a>Installatie van een mislukte update opnieuw uitvoeren  

Wanneer een update niet kan worden geïnstalleerd, bekijkt u de feedback in de console om oplossingen voor waarschuwingen en fouten te identificeren. Bekijk de **ConfigMgrPrereq. log** op de site server voor meer informatie. Voordat u de installatie van een update opnieuw probeert uit te voeren, moet u fouten oplossen en waarschuwingen herstellen.  

> [!TIP]  
> Als er problemen zijn bij het downloaden of repliceren van een update, gebruikt u het [hulp programma voor het opnieuw instellen](update-reset-tool.md)van de update.  

Wanneer u klaar bent om de installatie van een update opnieuw uit te voeren, selecteert u de mislukte update en kiest u vervolgens een toepasselijke optie. Het gedrag voor opnieuw proberen van de update-installatie is afhankelijk van het knoop punt waar u de nieuwe poging start en de optie opnieuw gebruiken die u gebruikt.  

### <a name="retry-installation-for-the-hierarchy"></a>De installatie voor de hiërarchie opnieuw uitvoeren

Voer de installatie van een update voor de gehele hiërarchie opnieuw uit wanneer die update een van de volgende statussen heeft:  

- Controles van vereisten die zijn door gegeven met een of meer waarschuwingen en de optie voor het negeren van waarschuwingen voor controle van vereisten zijn niet ingesteld in de wizard bijwerken. (De waarde van de update voor de **waarschuwing vereisten negeren** in het knoop punt **updates en onderhoud** is **Nee**.)

- De vereiste is mislukt

- De installatie is mislukt  

- De replicatie van de inhoud naar de site is mislukt

Ga naar de werk ruimte **beheer** en selecteer het knoop punt **updates en onderhoud** . Selecteer de update en kies een van de volgende opties:  

- **Opnieuw proberen**: wanneer u het **opnieuw probeert** uit te voeren vanaf **updates en onderhoud**, wordt de installatie van de update opnieuw gestart en worden waarschuwingen over vereisten automatisch genegeerd. Als inhouds replicatie eerder is mislukt, repliceert de inhoud voor de update opnieuw.  

- **Waarschuwingen over vereisten negeren**: als de installatie van de update stopt vanwege een waarschuwing, kunt u **waarschuwingen voor vereisten negeren**selecteren. Met deze actie kan de installatie van de update na een paar minuten worden voortgezet en wordt de optie gebruikt om waarschuwingen over vereisten te negeren.

### <a name="retry-installation-for-the-site"></a>De installatie voor de site opnieuw uitvoeren

Voer de installatie van een update op een specifieke site opnieuw uit wanneer die update een van de volgende statussen heeft:  

- Controles van vereisten die zijn door gegeven met een of meer waarschuwingen en de optie voor het negeren van waarschuwingen voor controle van vereisten zijn niet ingesteld in de wizard bijwerken. (De update waarde voor de **waarschuwing ignore vereisten** in het knoop punt updates en onderhoud is **Nee**.)  

- De vereiste is mislukt

- De installatie is mislukt

Ga naar de werk ruimte **bewaking** en selecteer het knoop punt **site onderhoud status** . Selecteer de update en kies een van de volgende opties:  

- **Opnieuw proberen**: wanneer u de **status van de site Servicing**opnieuw **probeert** , start u de installatie van de update alleen op die site opnieuw. In tegens telling tot het **uitvoeren van het** knoop punt **updates en onderhoud** , worden waarschuwingen over vereisten niet genegeerd.  

- **Waarschuwingen over vereisten negeren**: als de installatie van de update stopt vanwege een waarschuwing, kunt u **waarschuwingen voor vereisten negeren**selecteren. Met deze actie kan de installatie van de update na een paar minuten worden voortgezet en wordt de optie gebruikt om waarschuwingen over vereisten te negeren.  

## <a name="after-a-site-installs-an-update"></a><a name="bkmk_after"></a>Nadat een site een update heeft geïnstalleerd  

Nadat de site is bijgewerkt, controleert u de controle lijst na de update voor de betreffende versie:  

- [Controle lijst na de update voor versie 2002](checklist-for-installing-update-2002.md#post-update-checklist)

- [Controle lijst na de update voor versie 1910](checklist-for-installing-update-1910.md#post-update-checklist)  

- [Controle lijst na de update voor versie 1906](checklist-for-installing-update-1906.md#post-update-checklist)  

- [Controle lijst na de update voor versie 1902](checklist-for-installing-update-1902.md#post-update-checklist)  

## <a name="enable-optional-features-from-updates"></a><a name="bkmk_options"></a>Optionele functies van updates inschakelen  

Wanneer een update een of meer optionele functies bevat, hebt u de mogelijkheid om die functies in uw hiërarchie in te scha kelen. Schakel functies in wanneer de update wordt geïnstalleerd of ga later terug naar de-console om de optionele functies in te scha kelen.

Als u beschik bare functies en hun status wilt weer geven, gaat u in de-console naar de werk ruimte **beheer** , vouwt u **updates en onderhoud**uit en selecteert u het knoop punt **functies** .

Wanneer een functie niet optioneel is, wordt deze automatisch geïnstalleerd. Deze wordt niet weer gegeven in het knoop punt **functies** .  

> [!Important]  
> Schakel in een hiërarchie met meerdere sites alleen optionele functies of voorlopige versies in vanaf de centrale beheer site. Dit gedrag zorgt ervoor dat er geen conflicten zijn tussen de hiërarchie. <!--507197-->  

Wanneer u een nieuwe functie of voorlopige functie inschakelt, moet de Configuration Manager hiërarchie beheerder (HMAN) de wijziging verwerken voordat deze functie beschikbaar wordt. De verwerking van de wijziging is vaak direct. Afhankelijk van de HMAN-verwerkings cyclus kan het tot 30 minuten duren voordat deze is voltooid. Nadat de wijziging is verwerkt, start u de console opnieuw op voordat u de functie kunt gebruiken.

Vanaf versie 2002,<!--5834830--> Wanneer er nieuwe Cloud functies beschikbaar zijn in het beheer centrum van micro soft Endpoint Manager of door andere gekoppelde cloud services voor uw on-premises Configuration Manager-installatie, kunt u zich nu aanmelden bij deze nieuwe functies in de Configuration Manager-console.

### <a name="list-of-optional-features"></a>Lijst met optionele functies

De volgende functies zijn optioneel in de meest recente versie van Configuration Manager:<!--505213-->  

<!--Note to include in target articles

> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](install-in-console-updates.md#bkmk_options).  

-->

- [Community-hub](community-hub.md)<!--3555935, C098DA03-C33C-4E15-B337-6C0FEEB3CB8A-->
- [BitLocker-beheer](../../../protect/plan-design/bitlocker-management.md) <!-- 3601034,6DD56E46-C3EC-4E38-A16F-E98644BB6434 -->
- [Resultaten van verzamelings lidmaatschap synchroniseren met Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->
- [Detectie van gebruikers groepen Azure Active Directory](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->
- [Toepassings groepen](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D-->
- [Fout opsporing voor taken reeksen](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71-->
- [Pakket conversie beheer](../../../apps/pcm/package-conversion-manager.md) <!--1357861,4E0C09AF-7FC1-4412-A8BB-166D9BCD0093-->
- [Client-apps voor gezamenlijk beheerde apparaten](../../../comanage/workloads.md#client-apps) (voorheen bekend als *mobiele apps voor gezamenlijk beheerde apparaten*) <!--1357892,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C-->
- [Software-updates van derden](../../../sum/deploy-use/third-party-software-updates.md)<!--1357605,1352101,1358714;B5E192AE-C81F-4348-9EF9-07A3C0FBE597-->
- [Toepassings aanvragen voor gebruikers per apparaat goed keuren](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings) <!--1357015,4BA987C9-08FC-48E2-BFFE-C9DCF35B496A-->  
- [Scripts maken en uitvoeren](../../../apps/deploy-use/create-deploy-scripts.md) <!--1236459,566F8720-F415-4E10-9A51-CDE682BA2B2E-->
- [Updates van Surface-Stuur Programma's](../../../sum/get-started/configure-classifications-and-products.md) <!--1098490,82AD973A-7CDF-4B67-A665-72875D6E099A-->
- [Cloudbeheergateway](../../clients/manage/cmg/plan-cloud-management-gateway.md) <!--1101764,DD043119-789C-4158-AC79-725E999F385A-->
- [PFX maken](../../../protect/deploy-use/introduction-to-certificate-profiles.md) <!--1321368,CED76B79-929C-4C45-981F-B9BCA6D38A17-->
- [Azure Log Analytics-connector](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm) <!--1258052,73A7EC4D-EF22-4EA4-82A9-419C2A8CFC4D-->
- [Windows Defender exploit Guard-beleid](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md) <!--1355468,8491D4C8-8484-46B8-BCD6-17DC2CADBAEB-->
- [VPN voor Windows 10](../../../protect/deploy-use/vpn-profiles.md) <!--1283610,EDBEBA3D-3A4D-4465-84D9-D71EB811E7F6-->
- [Onderhoud van een cluster bewuste verzameling (Server groepen)](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697-->
- [Windows hello voor bedrijven](../../../protect/deploy-use/windows-hello-for-business-settings.md) (voorheen bekend als *Pass Port for work*) <!--1245704,8BCA2642-3719-4862-A355-9D39C979E1B4-->

> [!Tip]  
> Zie [functies van voorlopige versies](pre-release-features.md)voor meer informatie over functies die toestemming nodig hebben om in te scha kelen.  
>
> Zie [Technical Preview](../../get-started/technical-preview.md)voor meer informatie over functies die alleen beschikbaar zijn in de vertakking Technical Preview.

## <a name="use-pre-release-features-from-updates"></a><a name="bkmk_prerelease"></a>Functies van voorlopige versies van updates gebruiken

De huidige vertakking bevat functies van de voorlopige versie voor vroege test doeleinden in een productie omgeving. Zie functies van de [voorlopige versie](pre-release-features.md)voor meer informatie.

## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a>Veelgestelde vragen

### <a name="why-dont-i-see-certain-updates-in-my-console"></a>Waarom zie ik bepaalde updates niet in mijn console?

Als u een specifieke update niet kunt vinden in uw-console nadat de synchronisatie met de micro soft-Cloud service is voltooid, kan dit een van de volgende oorzaken hebben:  

- Voor de update is een configuratie vereist die uw infra structuur niet gebruikt, of uw huidige product versie voldoet niet aan een vereiste voor het ontvangen van de update.  

    Als u denkt dat u de vereiste configuraties en vereisten hebt voor een ontbrekende update, controleert u of het service aansluitpunt zich in de online modus bevindt. Gebruik vervolgens de optie **controleren op updates** in het knoop punt **updates en onderhoud** om een controle af te dwingen. Als uw service verbindings punt zich in de offline modus bevindt, gebruikt u het hulp programma voor service verbindingen om hand matig te synchroniseren met de Cloud service.  

- Uw account beschikt niet over de juiste beheer machtigingen op basis van rollen om updates in de Configuration Manager-console weer te geven. Zie [machtigingen voor het beheren van updates](#assign-permissions-to-view-and-manage-updates-and-features)voor meer informatie.  
